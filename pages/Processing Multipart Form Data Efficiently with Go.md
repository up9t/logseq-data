- Let's start by using this HTML code
-
- ```html
  <form action="http://localhost:8080/upload" method="POST" enctype="multipart/form-data">
    <label for="file-upload">Choose files to upload:</label>
    <input type="file" id="file-upload" name="file" multiple />
    <button type="submit">Upload</button>
  </form>
  ```
- This will submit to our backend server at `/upload` endpoint with method `POST`.
- We'll write down basic Go codes using the `net/http` standard library.
-
- ```go
  package main
  
  import "net/http"
  
  func main() {
    http.HandleFunc("POST /upload", func(w http.ResponseWriter, r *http.Request) {
      // code goes here.
    })
    
    http.ListenAndServe(":8080", nil)
   }
  
  ```
-
- The code we first want to write is the maximum amount of payload the client can send to our endpoint, we can use `http.MaxBytesReader` and assign it back to the `r.Body`. This worked because both `r.Body` and the return type of `http.MaxBytesReader` are both `io.ReadCloser` which is implemented the `io.Reader` and `io.Closer`.
  id:: 6a681cd1-e5eb-4fb4-a529-ca5878ac7346
- ```go
  const maxUploadSize = 2 * 1024 * 1024 // 2MB
  
  r.Body = http.MaxBytesReader(w, r.Body, maxUploadSize)
  ```
- And then we're going to retrieve the reader from the network directly with `r.MultipartReader`. We can use this to consume the data directly from Client->TCP Stream->Our App. This means we don't have to store the file to the disk first to read the content of it, we can just read the data directly, and then if necessary store it later to disk or memory.
- ```go
  reader, err := r.MultipartReader()
  ```
- Next thing is to get each part of data in the payload with `reader.NextPart`. We're going to need to wrap it in for loop because it has multiple parts, and stop the loop after it reach the end and no more data left, in Go we called this End Of File (EOF) to indicate there is no data left to read. One important note here is to not use `Goroutine` to read the data from the client, because TCP works sequentially, and after we call `reader.NextPart` it will automatically drop the data in the previous part.
- ```go
  for {
    part, err := reader.NextPart()
    
    if err == io.EOF {
      break
    }
    
    // another code goes here
  }	
  ```
- Then we're going to filter the part that only matches our key.
- ```go
  // this should be the same as the html input "name" attribute
  // here is an example
  // <input type="file" name="THIS_IS_THE_KEY" multiple />
  key := "THIS_IS_THE_EKY"
  
  if part.FormName() != key {
    part.Close()
    continue
  }
  
  ```
- After that we want to store the file to the disk. Start by creating a new file in our server with the same name as the client filename using `os.Create`.
-
- ```go
  filename := filepath.Base(part.FileName())
  
  dest, err := os.Create(filename)
  ```
- And here's the most important part, is to use `io.Copy`. It streams the data from `io.Reader` to `io.Writer` directly, uses almost-zero memory allocation. So from Client->TCP->Disk, using 32KB of memory only!
- ```go
  _, err = io.Copy(dest, part)
  
  // don't forget to close.
  part.Close()
  dest.Close()
  
  ```
-
-
- #go #web
-