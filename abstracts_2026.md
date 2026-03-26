# 1

Density estimation for tabular data is a crucial component of anomaly detection, sample generation, and clustering tasks. However, existing methods typically require costly training for each new dataset, limiting their practical applicability. We propose "OUR", a novel approach to density estimation that leverages the in-context learning paradigm, eliminating the need for retraining. Across multiple downstream tasks, our method achieves performance on par with state-of-the-art approaches, while offering significantly reduced inference time. These results highlight the potential for a paradigm shift from dataset-specific training to a unified foundation model for tabular density estimation.

# 2

Interpretability remains a fundamental challenge in deploying modern machine learning models in real-world settings. Existing explanation approaches require access to the full training dataset, which is often prohibitively large and memory-intensive to store and process. As a result, current methods suffer from limited scalability and practical applicability. To overcome these limitations, we introduce EPIC, a prototype-based explanation framework that eliminates the need for explicit dataset access during explanation generation. EPIC leverages generative models to synthesize realistic and semantically meaningful prototypes that approximate the underlying data distribution while enabling faithful model interpretation. Extensive experiments demonstrate that our framework captures key concepts in a human-understandable manner and produces high-quality explanations without degrading the predictive performance of the pretrained backbone model. Moreover, EPIC substantially reduces memory requirements, making explanation generation feasible in resource-constrained environments. Our results suggest that generative prototype learning provides a scalable and effective paradigm for dataset-free explainability, opening new directions for interpretable machine learning at scale.

# 3

Predicting system-wide travel time within complex urban networks under fluctuating spatiotemporal demand patterns remains a significant challenge. 
Existing methods, primarily grounded in Graph Neural Networks, are largely restricted to static topological features and localized detector data; consequently, they lack the flexibility to generalize across varying demand patterns.
In this work, we propose AVTTP (Assignment-Varying Travel Time Predictor), machine learning framework that trains the microscopic relationships between high-dimensional assignment patterns and global network performance (travel times) on a large-scale dataset comprising 100,000 diverse assignment patterns across three distinct urban topologies from the URB benchmark.
Our findings demonstrate that AVTTP effectively surrogates computationally expensive traffic micro simulators like SUMO. Our framework opens avenues towards microscopic assignments optimization.

# 4

Selectively erasing targeted concepts in large computer vision models remains challenging because dense concept entanglement inherently links unwanted features with essential retained knowledge. Existing machine unlearning approaches typically manipulate static weight spaces, causing collateral damage to the model's general utility, or rely on computationally expensive parameter-expanding modules. We propose BARRIER (Bounded Activation Regions for Robust Information Erasure), an architecture-agnostic framework that leverages Singular Value Decomposition and Interval Arithmetic to project hidden layer activations into a low-rank subspace and establish explicit geometric bounds around retained representations. Across discriminative classification and text-to-image diffusion models, the method effectively eradicates targeted visual classes and explicit content while maintaining robust test accuracy and generative quality, outperforming state-of-the-art weight-centric baselines without adding trainable parameters. These results demonstrate that explicitly bounding functional drift in the dynamic activation space provides a theoretically grounded and highly efficient mechanism for surgical concept suppression.

# 5

Integrating physics-based simulation with 3D Gaussian Splatting remains a challenge. Existing
solutions typically utilize computationally heavy meshing mechanisms or use first-order
approximations of the deformation map, which requires access to the internal states of the
physical simulator. We propose GASP , a pipeline for integration of physics-based simulations
with Gaussian Splatting using parametrized flat Gaussian distributions. Consequently, the
problem of modeling Gaussian primitives using the physics engine is reduced to working with a
collection of 3D points, allowing any physics engine to control the simulation. We evaluated the
proposed pipeline on a set of synthetic objects and complex real-world scenes. Our results
indicate that the visual quality of GASP is comparable to state-of-the-art methods in terms of
FID scores and using the Gaussian grouping mechanism more than doubles the rendering
speed. Our findings demonstrate that high-fidelity physical simulations can be achieved without
the need for differentiable simulators or mesh-based proxies.

# 6

Preference-alignment methods such as RLHF are used to make large language models (LLMs) more helpful and safe, but they can also induce unintended behavioral tendencies, including forms of reward hacking. Although prior work has documented such emergent effects at the behavioral level, the internal mechanisms by which alignment training produces them remain poorly understood. In this work, we investigate whether these behaviors can be explained as updates concentrated on specific internal representations, which we call assistant personas. We analyze the circuits associated with these representations and study their causal role through targeted interventions. Our results show that ablating persona-related circuits can suppress particular side effects of alignment training while largely preserving the model’s general capabilities, whereas amplifying these circuits makes the corresponding behaviors more pronounced. These findings suggest that at least some emergent alignment behaviors are mechanistically localized, opening the door to more precise, predictable, and controllable interventions aimed at making LLMs better aligned with human preferences.<img width="451" height="218" alt="image" src="https://github.com/user-attachments/assets/30d105d3-a24d-469d-bd5c-7c6d41ddd13d" />

