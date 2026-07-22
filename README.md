### Note on LoRA configuration across models

The SFT scripts for Gemma-2, Phi-2, Qwen, and TinyLlama share the same
training hyperparameters (batch size, gradient accumulation, epochs,
learning rate). The only intentional difference is `target_modules` in
`LoraConfig`, which depends on each model's internal layer naming:

| Model family      | target_modules                                      |
|-------------------|--------------------------------------------------------|
| Gemma-2 / Phi-2    | q_proj, k_proj, v_proj, dense, fc1, fc2              |
| Qwen / TinyLlama   | q_proj, k_proj, v_proj, o_proj                       |

This difference is required because these architectures use different
names for their attention output and MLP projection layers. It is not
an inconsistency between scripts. All other hyperparameters are held
constant across models to keep the comparison fair.
