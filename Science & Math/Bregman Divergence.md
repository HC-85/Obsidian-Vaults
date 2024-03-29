Measure of difference between two points defined in terms of a strictly [[Convexity|convex]] function. If these points are probability distributions, it results in a [[Statistical Distance|statistical distance]].
Some properties:
- They never satisfy the triangle inequality.
- Not all satisfy symmetry.
- They do satisfy a generalization of the Pythagorean theorem.
- Their statistical manifold is [[Dually Flat Manifold|dually flat]].

Let $F:\Omega\rightarrow\mathbb{R}$ be a continuously-differentiable, strictly convex function defined on the [[Convex Set|convex set]] $\Omega$. The Bregman divergence generated by $F$ for $q,p\in\Omega$ is the difference between $F$ at $p$ and the first-order Taylor expansion of $F$ around $q$ at $p$:
$$
D_{F}=[F(p)]-[F(q)+\langle \nabla F(q),p-q\rangle]
$$
#DontGetIt 