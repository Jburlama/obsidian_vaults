- https://raytracing.github.io/

- The one thing that all ray tracers have is a ray class and a computation of what color is seen along a ray. Let’s think of a ray as a function $P(t)=A+tb$. Here $P$ is a 3D position along a line in 3D. $A$ is the ray origin and b is the ray direction. The ray parameter $t$ is a real number (double in the code). Plug in a different $t$ and $P(t)$ moves the point along the ray. Add in negative $t$ values, and you can go anywhere on the 3D line. For positive $t$, you get only the parts in front of $A$, and this is what is often called a half-line or a ray. 

![[fig-1.02-lerp.jpg]]
