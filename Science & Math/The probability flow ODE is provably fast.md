#Paper #SDE #ODE #DDPM 
Denoising diffusion probabilistic models (DDPMs) reverse the diffusion process as a [[Stochastic Differential Equation|stochastic differential equation]] (SDE) whose coefficients are learned via neural network training and the statistical technique of [[Score Matching|score matching]].

Instead of implementing the time reversed diffusion as an SDE, it can be implemented with a probability flow ODE. 
