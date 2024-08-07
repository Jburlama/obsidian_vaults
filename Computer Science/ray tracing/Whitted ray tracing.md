- file:///home/jhonas/Downloads/Jamis%20Buck%20-%20The%20Ray%20Tracer%20Challenge-Pragmatic%20Bookshelf%20(2019)-1.pdf
- [[maping floats to pixels]]

- a recursive ray tracing that in a nutshell the algorithm works like this for each of the image’s pixels:

	1. Cast a ray into the scene, and find where it strikes a surface.
	
	2. Cast a ray from that point toward each light source to determine which	lights illuminate that point.
	
	3. If the surface is reflective, cast a new ray in the direction of reflection a recursively determine what color is reflected there.
	
	4. If the surface is transparent, do the same thing in the direction of refraction.
	
	5. Combine all colors that contribute to the point (the color of the surface, the reflection, and refraction) and return that as the color of the pixel.

# Tuples, Points and vector

[[vetores]]

- A tuple is just an ordered list of things, like numbers.

- To differentiate vectors from points, we will add a parameter called w that will be 0 or 1, 1 being a point and 0 being a vector.

	**(4, -4, 3, 1), this is a point with coordinates XYZ: 4,-4,3.
	(-4, 4, -3, 0), this is a vector where the XYZ coordinates are the the origin point relative to an end point.**
	

	![[Captura de ecrã de 2024-07-24 19-23-09.png]]
##  Comparing floating points
![[Captura de ecrã de 2024-07-24 19-23-36.png]]

## Operations

### Adding tuples
	![[Captura de ecrã de 2024-07-24 19-32-15.png]]

### Subtracting tuples
	![[Captura de ecrã de 2024-07-24 19-34-18.png]]

- Similarly, you can subtract a vector (w of 0) from a point (w of 1) and get another tuple with a w of 1—a point. Conceptually, this is just moving backward by the given vector.

	![[Captura de ecrã de 2024-07-24 19-36-23.png]]

- Lastly, subtracting two vectors gives us a tuple with a w of 0—another vector, representing the change in direction between the two.

	![[Captura de ecrã de 2024-07-24 19-39-15.png]]

- As with addition, though, not every combination makes sense. For instance, if you subtract a point (w = 1) from a vector (w = 0), you’ll end up with a negative w component, which is neither point nor vector.

### Negating tuples

- Sometimes you’ll want to know what the opposite of some vector is. That is to say, given a vector that points from a surface toward a light source.
-  Mathematically, you can get it by subtracting the vector from the tuple (0, 0, 0, 0).

	![[Captura de ecrã de 2024-07-24 19-54-05.png]]
	
- You can simplify this by implementing a negate operation, which negates each component of the tuple.

	![[Captura de ecrã de 2024-07-24 19-55-48.png]]

### Scalar Multiplication and Division

- Now let’s say you have some vector and you want to know what point lies 3.5 times farther in that direction. It turns out that multiplying the vector by 3.5 does just what you need. The 3.5 here is a scalar value because multiplying by it scales the vector (changes its length uniformly). To do it, you multiply each component of the tuple by the scalar. 

	![[Captura de ecrã de 2024-07-24 20-07-02.png]]

	![[Captura de ecrã de 2024-07-24 20-08-20.png]]
	
- Note that last test, where you multiply the tuple by 0.5. This is essentially the same thing as dividing the tuple by 2.
- You can always implement division with multiplication, but sometimes it’s simpler to describe an operation as division.

	![[Captura de ecrã de 2024-07-24 20-10-27.png]]

### Magnitude

- The distance represented by a vector is called its magnitude, or length. It’s how far you would travel in a straight line if you were to walk from one end of the vector to the other.

	![[Captura de ecrã de 2024-07-24 20-17-53.png]]


	![[Captura de ecrã de 2024-07-24 20-18-25.png]]

- Vectors with magnitudes of 1 are called a unit vectors, and these will be super handy.

### Normalization

- Normalization is the process of taking an arbitrary vector and converting it into a unit vector. It will keep your calculations anchored relative to a common scale (the unit vector), which is pretty important. If you were to skip normalizing your ray vectors or your surface normal, your calculations would be scaled differently for every ray you cast, and your scenes would look terrible (if they rendered at all).

	![[Captura de ecrã de 2024-07-24 20-28-28.png]]
	
	[[Fast inverse square root]]

### Dot product
	
	[[Vetores - Produto Escalar (Multiplicação entre vetores)]]
	https://betterexplained.com/articles/vector-calculus-understanding-the-dot-product/	

- When dealing with vectors, a dot product (also called a scalar product, or inner product) is going to turn up when you start intersecting rays with objects, as well as when you compute the shading on a surface. The dot product takes two vectors and returns a scalar value.

	![[Captura de ecrã de 2024-07-24 20-31-58.png]]

-  The smaller the dot product, the larger the angle between the vectors. For example, given two unit vectors, a dot product of 1 means the vectors are identical, and a dot product of -1 means they point in opposite directions. More specifically, and again if the two vectors are unit vectors, the dot product is actually the cosine of the angle between them.

	![[Captura de ecrã de 2024-07-24 23-36-36.png]]

### Cross Product

- The cross product is another vector operation, but unlike the dot product, it returns another vector instead of a scalar.

	![[Captura de ecrã de 2024-07-24 23-42-29.png]]
	![[Captura de ecrã de 2024-07-24 23-45-02.png]]



# Matrices

- A matrix is a grid of numbers that you can manipulate as a single unit. For  example, here’s a 2x2 matrix. It has two rows and two columns.
		| 3 1 |
		| 2 7 |

- And here’s a 3x5 matrix, with three rows and five columns:
		| 9 1 2 0 3 |
		| 0 0 2 3 1 |
		| 8 7 5 4 6 |
		
- during the project we will be doing lots of matrix operations we should be able to compare them.
	![[Screenshot from 2024-07-27 17-55-44.png]]
	![[Screenshot from 2024-07-27 17-56-31.png]]

## Multiplying Matrices

- https://betterexplained.com/articles/linear-algebra-guide/
- [https://betterexplained.com/articles/matrix-multiplication/]()
- Multiplication is the tool you’ll use to perform transformations like scaling, rotation, and translation.

	![[Screenshot from 2024-07-27 18-03-53.png]]
	![[Screenshot from 2024-07-27 18-05-42.png]]

- Multiplying a matrix by a tuple produces another tuple.
- we treat the tuple like a one column matrix.
	![[Screenshot from 2024-07-27 18-09-02.png]]
	![[Screenshot from 2024-07-27 18-10-06.png]]

## The Identity Matrix

- If you multiply any number by 1 you get the number itself. For that reason 1 is considered the identity.
- The same applies for matrix, if you multiply the matrix for the identity, you get the matrix itself.
	![[Screenshot from 2024-07-28 18-06-55.png]]
	![[Screenshot from 2024-07-28 18-08-24.png]]

## Transposing Matrices

- To transpose a matrix means that the rows becomes the columns and the columns becomes the rows.

	![[Screenshot from 2024-07-28 18-21-48.png]]

- And interestingly, the transpose of the identity matrix always gives you the identity matrix.

## Inverting Matrices

- inversion is the operation that allows you to reverse the effect of multiplying by a matrix.
- we can use the inverted matrix to solve for situations where divisions would be necessary.
- Inverting matrices is the key to transforming and deforming shapes in a ray tracer.
- if we multiply matrix A by the inverse of A, we get the identity matrix.
- **If a matrix have a determinant equal to zero, then we cannot determine the inverse, because we would be dividing by 0. Such a matrix is called a singular matrix.**

- ==STEP1:== Find the determinant.
- ==STEP2:== Find the matrix of cofactors.
- ==STEP3:== Transpose the cofactor matrix.
- ==STEP4:== Divide each element of the cofactor matrix by the determinant of the original matrix.

	![[Screenshot from 2024-07-30 16-33-50.png]]
	![[Screenshot from 2024-07-30 16-41-39.png]]

- *This part of the code is important to be working correctly, here are some test to make sure everything is working has intended.*

	![[Screenshot from 2024-07-30 16-45-52.png]]
	![[Screenshot from 2024-07-30 16-46-33.png]]

### Determining Determinants

- The determinant is one of the pieces that we'll use to determine the inverse of a matrix.
- this is how to determine the determinant of a 2×2 matrix.

	![[Screenshot from 2024-07-28 19-39-00.png]]

- to determine the determinant of a 3×3 matrix we need first to determine the minor of any row, then multiplied by the element in the following formula.
		$(0,0)*minor(0,0) - (0,1)*minor(0,1) + (0,2)*minor(0,2)$
- or alternately can use the cofactor:
		$(0,0)*cofactor(0,0) + (0,1)*cofactor(0,1) + (0,2)cofactor(0,2)$
- this also works for 4×4 matrix.
	![[Screenshot from 2024-07-29 18-35-15.png]]
	![[Screenshot from 2024-07-29 18-36-20.png]]


### Spotting Submatrices

- A submatrix is what is left when you delete a single row and column from a matrix.
	![[Screenshot from 2024-07-28 19-42-42.png]]

### Manipulating Minors

- a Minor is the determinant of a submatrix.
	![[Screenshot from 2024-07-28 19-49-18.png]]


### Computing Cofactors

- cofactors are minors that have their signed (possibly) changed.
- you consider that row and column to determine whether to negate the result.
	![[Screenshot from 2024-07-28 21-48-50.png]]
	![[Screenshot from 2024-07-28 21-49-18.png]]

- if row + column is an odd number, then you negate the minor. Otherwise, you just return the minor as is.

# Matrix transformations

## Translation

- Translation is a transformation that moves a point by adding the translation matrix.

	![[Screenshot from 2024-07-30 18-22-15.png]]

- If you take the inverse of a translation matrix, you make another translation matrix, that moves the point in reverse.
	![[Screenshot from 2024-07-30 18-24-27.png]]


	![[Screenshot from 2024-07-30 18-04-56.png]]
	
- Translation matrices cannot move vectors, only points, the reason for that will be the w component that is set to 0 for vectors, and that will cause the translation to be ignored, when multiplied by a vector.

	![[Screenshot from 2024-07-30 18-27-20.png]]

## Scaling

- Where translation moves a point by adding to it, scaling moves it by multiplication.
- When applied to an object centered at the origin, this transformation scales all points on the object, effectively making it larger (if the scale value is greater than 1) or smaller (if the scale value is less than 1).
	![[Screenshot from 2024-07-30 19-48-24.png]]

- Scaling applies to vectors as well, changing their length.
	![[Screenshot from 2024-07-30 19-49-53.png]]

- Multiplying a tuple by the inverse of a scaling matrix will scale the tuple in the opposite way.
	![[Screenshot from 2024-07-30 19-51-53.png]]

- *Constructing a scaling matrix:*
	![[Screenshot from 2024-07-30 19-53-48.png]]

## Reflection

- Reflection is a transformation that takes a point and reflects it, moving it to the other side of an axis.
- Reflection is essentially the same thing as scaling by a negative value.

	![[Screenshot from 2024-07-30 19-59-50.png]]

## Rotation

- Multiplying a tuple by a rotation matrix will rotate that tuple around an axis.
- Each of the three axes requires a different matrix to implement the rotation.

	[[CÍRCULO E CIRCUNFERÊNCIA]]

### Rotation around the X axis

- This first rotation matrix rotates a tuple some number of radians around the x axis.

	![[Screenshot from 2024-07-30 20-41-41.png]]

- The inverse of a rotation matrix, will rotate in the opposite direction.

	![[Screenshot from 2024-07-30 20-48-49.png]]

- *The transformation matrix for rotating around the x axis is construct like the following:*
	![[Screenshot from 2024-07-30 20-59-50.png]]

### Rotating around the Y axis

- The y axis rotation works just like the x axis rotation, only changing the y axis.

	![[Screenshot from 2024-07-30 21-02-47.png]]

- *The transformation matrix for rotating around the y axis is construct like the following:*
	![[Screenshot from 2024-07-30 21-04-19.png]]

### Rotating around the Z axis

- the z axis rotation woks just like the previous rotations, only changing the z axis.

	![[Screenshot from 2024-07-30 21-06-07.png]]

- *The transformation matrix for rotating around the z axis is constructed like the following:*
	![[Screenshot from 2024-07-30 21-07-12.png]]

## Chaining Transformations
 - We can do multiple transformations at the same time, like the following:
	![[Screenshot from 2024-07-30 21-39-12.png]]

- or we can do like the following because matrix multiplication is associative:
	![[Screenshot from 2024-07-30 21-41-16.png]]

- but matrix multiplication is not commutative, so the order of operations matters.
		-  *A * B  is not the same as B * A.*
# Ray-Sphere Intersections

- Ray casting is the process of creating a ray, or line, and finding the intersections of that ray with the objects in a scene.

## Creating Rays

- Each ray will have a stating point called the origin, and a vector, called direction which says here it points.
	![[Screenshot from 2024-07-31 20-03-01.png]]

- We can find any point that lies along the ray with t.
	![[Screenshot from 2024-07-31 20-05-25.png]]

- To find the position, you multiply the ray’s direction by t to find the total distance traveled, and then add that to the ray’s origin.
	![[Screenshot from 2024-07-31 20-06-38.png]]
	![[Screenshot from 2024-07-31 20-08-46.png]]

## Intersecting Rays with Spheres

- **Given a sphere with its center at the point (0,0,0) with radius of 1.**
- **A ray with origin point (0,0,-5) and a direction vector (0,0,1).**

- The ray should intersect the sphere at (0,0,-1) and (0,0,1), 4 and 6 units respectively away from its origin point.
- If the same ray move 1 point in the y direction, it will intersect the sphere at the tangent.
- If the ray move just a bit int the y direction, it should miss the sphere, not intersecting at all.
- If the originates inside the sphere, it should have one intersection point in front and another behind the ray.
- If the sphere is completely behind the ray we should get two intersection with negative values.

### Discriminant

- To see if the ray intersects the sphere, we will join the vector equation with the sphere equation.
	- $P(t) = O + Dt$
	- $(p - c)^2 = r^2$
	- $(P(t) - c)^2 = r^2$
	
	[[Formula quadratica]]
	https://en.wikipedia.org/wiki/Line%E2%80%93sphere_intersection
	https://www.scratchapixel.com/lessons/3d-basic-rendering/minimal-ray-tracer-rendering-simple-shapes/ray-sphere-intersection.html
	
- Start by computing the discriminant — A number that tell you whether the ray hits the sphere or not.
	![[Screenshot from 2024-08-01 16-47-28.png]]

- If the discriminant is negative than the ray misses the sphere.
- Otherwise we'll see two intersection or one, if the ray hits the sphere at the tangent.
	![[Screenshot from 2024-08-01 16-56-01.png]]
- If the ray intersects at the tangent both t1, and t2 will be the same value.

### Tracking Intersections

- The intersection data structure will aggregate:
	1. The t value of the intersection, and
	2. The object that was intersected.
	
	![[Screenshot from 2024-08-01 20-11-39.png]]

- You’ll also need a way to aggregate these intersection objects so you can work with multiple intersections at once.
	![[Screenshot from 2024-08-01 20-15-09.png]]

### Identifying hits

- The hit will never be behind the ray’s origin, since that’s effectively behind the camera.
- the hit will always be the intersection with the lowest non-negative t value.

	![[Screenshot from 2024-08-04 18-52-25.png]]

### Transforming Rays and Spheres

- In other to transform the object, we need to change the relationship between the ray and the object. Therefore, we don't necessary need to move the object itself by the ray.

	![[Screenshot from 2024-08-06 17-26-14.png]]
	- You have to leave that vector with its new length, so that when the t value is eventually computed, it represents an intersection at the correct distance (in world space!) from the ray’s origin.

# Light and Shading

- To do this, you’ll add a source of light, and then implement a shading algorithm to approximate how brightly that light illuminates the surfaces it shines on.

- We will need 4 vectors.
	![[Screenshot from 2024-08-06 17-45-13.png]]
	*• E is the eye vector, pointing from P to the origin of the ray (usually, where the eye exists that is looking at the scene).
	• L is the light vector, pointing from P to the position of the light source.
	• N is the surface normal, a vector that is perpendicular to the surface at P.
	• R is the reflection vector, pointing in the direction that incoming light would bounce, or reflect.*

• To find E, you can negate the ray’s direction vector, turning it around to point back at its origin.
• To find L, you subtract P from the position of the light source, giving you the vector pointing toward the light.

## Surface Normal

### Computing the Normal on a Sphere

- The following function normal_at(sphere, point) will return the normal on the given sphere, at the given point.

	![[Screenshot from 2024-08-07 11-35-37.png]]

- Those vectors needs to be normalized.

	![[Screenshot from 2024-08-07 11-37-39.png]] 
	
	![[Screenshot from 2024-08-07 12-58-41.png]]

- Note that, because this is a unit sphere, the vector will be normalized by default for any point on its surface, so it’s not strictly necessary to explicitly normalize it here.
	![[Screenshot from 2024-08-07 13-02-26.png]]

### Transforming Normals

- If you were to naively apply the algorithm above to find the normal at almost any point on that sphere, you’d find that it no longer works correctly.

	![[Screenshot from 2024-08-07 13-04-46.png]]

- The sphere origin is no longer at the world center.

### Reflecting Vectors

- the case where a vector approaches a normal at a 45° angle, moving at equal speed in both x and y. It should emerge at a 45° angle, with its y component reversed.

	![[Screenshot from 2024-08-07 13-38-27.png]]
	
	![[Screenshot from 2024-08-07 13-39-36.png]]

### The Phong Reflection Model

- It simulates the interaction between three different types of lighting:

	-  *Ambient reflection is background lighting*
	- *Diffuse reflection is light reflected from a matte surface.*
	- *Specular reflection is the reflection of the light source itself and results in what is called a specular highlight—the bright spot on a curved surface.*
		
	![[Screenshot from 2024-08-07 15-08-35.png]]

#### light source

- Its defined by its intensity, or how bright it is. The intensity also describes the color of the light source.

	![[Screenshot from 2024-08-07 15-14-39.png]]







# References

- https://pragprog.com/titles/jbtracer/the-ray-tracer-challenge/
- https://betterexplained.com/articles/vector-calculus-understanding-the-dot-product/	
- https://betterexplained.com/articles/linear-algebra-guide/
- https://betterexplained.com/articles/matrix-multiplication/
- https://en.wikipedia.org/wiki/Line%E2%80%93sphere_intersection
- https://www.scratchapixel.com/lessons/3d-basic-rendering/minimal-ray-tracer-rendering-simple-shapes/ray-sphere-intersection.html
- https://forum.arduino.cc/t/floating-point-using-map-function/348113