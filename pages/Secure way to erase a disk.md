- There is probably a time where you want to wipe out your entire disk, maybe you don't need the disk anymore because you have a better replacement, or you want to send your laptop to a repair man, and you don't want him to see your disk content, that's actually a real story that I read on Reddit. Anyway, whatever your reason is, you should do it properly, before I tell you how to do that, let me give you a wrong, popular way on how to erase your disk. It's by using the `dd` command (on linux).
-
- `dd` command, stands for Data Duplicator, is a linux command to copy/duplicate data from one source to the other. The acronym is pretty self-explanatory. But some Linux Sysadmins would joke that command is actually the abbreviation for Disk Destroyer for a solid reason that it can erase your whole disk without warning if you make a simple mistake, so whoever uses this command should be very cautious. Let me give you some examples about this command.
-
- **This command copy the input file (if) to the output file (of).** The `/dev/sda` is actually a file on linux that represent a disk, so it's not actually a file. It could be `/dev/sda`, `/dev/nvme`, `/dev/sdb`, it depends on your system, you can list all the disk with the command `lsblk`.
- ```bash
  dd if=ubuntu.iso of=/dev/sda
  ```
- But you can change the input file and the output file to be whatever you want. For example, this command copies all the content in the `/dev/zero` to the `/dev/sda` which means it will fill the disk (`dev/sda`) with zeroes.
- ```bash
  dd if=/dev/zero of=/dev/sda
  ```
- While this sounds pretty good with our goal, it's actually not a reliable and secure way to erase a disk, because there are hidden parts in our disk that our Operating System (OS) can't see. Not even our `dd` command can delete that part.
-
- ## The reliable way
-
- Most disk manufacturers nowadays put a feature on their disk to be able to erase the disk securely using a specific protocol. You don't exactly need to know what protocol they use because usually they have made a button to do the erasing by just clicking it on the UEFI/BIOS menu. Or you can also download a certain utility on linux so you can erase it with CLI. There are two ways or algorithm on how the data will be erased: Voltage Spike and Cryptographic Encryption.
-
- **Voltage Spike**, this way your disk controller (not sure if that's the right word) will put a precise voltage amount to each cell in the disk. Literally clears out everything, but it takes quite some times because you can't just put a wave of voltage spike to the whole disk, that would burn the internal components. But instead they will be in turn.
- **Cryptographic Encryption**, First your disk need to be on self-encrypting mode, that mean every data is encrypted whenever they're being written to the disk (or something like that, should check the fact). When the disk is encrypted there is a key stored somewhere in there to be able to perform this encrypt and decrypt mechanism probably inside the disk's hidden part. What this method does is to simply delete that key, and make another key right after the deletion of the first key which makes the process instant. This immidiate key creation is so that you can reuse the disk again. But there is a question regarding of security, how secure is it as we know the data is still there. Actually it's very strong that it is impossible to crack it, even with quantum computers, the process would take way longer than the lifespan of the observable universe. They use AES-256 Encryption method which is known for its quantum-proof encryption. Honestly, I would trust my life on it.
-
-
-
- #disk