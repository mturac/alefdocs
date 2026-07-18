# Automatic Differentiation and Vectorization

Alef provides native language support for Automatic Differentiation (AutoDiff) and Vectorization, making it a powerful language for AI, machine learning, and numerical computing.

These capabilities are exposed through two built-in keywords: `grad` and `vmap`.

## `grad` - Automatic Differentiation

The `grad` keyword computes the gradient (derivative) of a function with respect to its inputs.

```alef
fn square(x: number): number {
    return x * x;
}

// Computes the derivative of square(x), which is 2*x
let d_square = grad(square);

println(d_square(3.0)); // Outputs: 6.0
println(d_square(4.0)); // Outputs: 8.0
```

`grad` can also be used inline as an expression:

```alef
let derivative = grad(fn(x) { return x * x * x; });
println(derivative(2.0)); // Outputs: 12.0 (3 * 2^2)
```

## `vmap` - Vectorization

The `vmap` keyword vectorizes a scalar function, allowing it to efficiently process arrays (tensors) of data without explicit loops.

```alef
fn add_one(x: number): number {
    return x + 1.0;
}

// Vectorize the add_one function
let v_add_one = vmap(add_one);

let data = [1.0, 2.0, 3.0];
let result = v_add_one(data);
println(result); // Outputs: [2.0, 3.0, 4.0]
```

## Combining `grad` and `vmap`

You can seamlessly combine `grad` and `vmap` to compute gradients over batches of data efficiently:

```alef
fn model(w: number, x: number): number {
    return w * x;
}

// Vectorize over data 'x', then take gradient with respect to weights 'w'
let batched_grad = vmap(grad(model));
```

This makes writing custom training loops and optimization algorithms incredibly expressive and fast directly in Alef!
