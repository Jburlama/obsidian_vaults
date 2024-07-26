- file:///home/jhonas/Downloads/Jamis%20Buck%20-%20The%20Ray%20Tracer%20Challenge-Pragmatic%20Bookshelf%20(2019)-1.pdf

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

### Dot product
	
	[[Vetores - Produto Escalar (Multiplicação entre vetores)]]
	https://betterexplained.com/articles/vector-calculus-understanding-the-dot-product/	

- When dealing with vectors, a dot product (also called a scalar product, or inner product) is going to turn up when you start intersecting rays with objects, as well as when you compute the shading on a surface. The dot product takes two vectors and returns a scalar value.

	![[Captura de ecrã de 2024-07-24 20-31-58.png]]

-  The smaller the dot product, the larger the angle between the vectors. For example, given two unit vectors, a dot product of 1 means the vectors are identical, and a dot product of -1 means they point in opposite directions. More specifically, and again if the two vectors are unit vectors, the dot product is actually the cosine of the angle between them

	![[Captura de ecrã de 2024-07-24 23-36-36.png]]

### Cross Product

- The cross product is another vector operation, but unlike the dot product, it returns another vector instead of a scalar.

	![[Captura de ecrã de 2024-07-24 23-42-29.png]]
	![[Captura de ecrã de 2024-07-24 23-45-02.png]]





# References
- https://raytracing.github.io/
- https://pragprog.com/titles/jbtracer/the-ray-tracer-challenge/