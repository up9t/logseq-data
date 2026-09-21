-
- PI or $$\pi$$ is a `ratio` of a circle circumference to its diameter. It's 3.14....
- Remember that $$\pi$$ is not equal to $$180 \degree$$. It's just 3.14......
-
- ## How can $$\pi$$ represent a half circle?
-
- First of all, let me introduce you to `radian`.
- `Radian` is a `unit` that represent an `ratio` of an arc length to its radius.
- For example, how many radians does the length of the arc. Say that the radius of the arc is 5cm and the arc length is 10cm, the answer would be 10/5 = `2 radians`.
-
- When it's converted to another unit called `degree` 1 radian would be around $$57.3 \degree$$.
- Because 1 radian only make up for about $$57.3 \degree$$, making a half circle need exactly $$\pi \times rad$$, which means $$3.14 \times rad$$.
- If you use calculator, that would be $$180 \degree$$. But we rarely use degree, so multiplication by radian to convert it to degree is redundant.
	-
- In computer, radian is mostly used instead of degree, so you can just use only $$\pi$$ to represent a half circle.
- In a system where degree is expected you can't use $$\pi$$ alone without `radian`, that would make it only 3.14 degree, not $$180 \degree$$. Which isn't going to make the half circle. Consider the example.
-
- ```typescript
  makeArcRadian(Math.PI); // correct; no need to multiply by radian again.
  
  makeArcDegree(180); // correct; direct degree value.
  makeArcDegree(Math.PI); // wrong! this would create a 3.14 degree arc instead.
  makeArcDegree(Math.PI * RADIAN); // correct, if radian is in 57.3 (degree).
  ```
-
- So, $$\pi$$ can represent as a half circle because, $$\pi \times rad = 180 \degree$$, and in a system where radian unit is expected, passing a value like 4 would automatically means `4 times radian` or `4 radians`, same with $$\pi$$ would be $$\pi rad$$.
-
-
- #math #circle
-
-