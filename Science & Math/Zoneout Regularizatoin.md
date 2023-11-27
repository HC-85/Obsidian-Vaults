Addresses some limitations of dropout, specifically for RNNs. 
Instead of dropping weights to zero, it sets them to a previous state.
$$
h_t = d_t\odot h_{t-1} + (1-d_t)\odot \tilde{h}_t
$$
Creates skip connections in time, helping with vanishing gradients.