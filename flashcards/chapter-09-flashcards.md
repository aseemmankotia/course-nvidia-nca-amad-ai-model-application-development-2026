## Chapter 9: Physical AI: Robotics, Simulation, and Digital Twins — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Define Physical AI in one sentence. | AI that perceives the real world through sensors and acts on it through actuators (e.g., robots, autonomous vehicles). Exam tip: contrast with generative AI, which stays in digital data space. |
| 2 | What is a digital twin? | A virtual, continuously-synced model of a physical system/asset used for monitoring, simulation, and prediction. Exam tip: it mirrors real-time data, not just a static 3D model. |
| 3 | Omniverse vs Isaac Sim — what's the key difference? | Omniverse is the broader platform for building physically accurate 3D virtual worlds/digital twins. Isaac Sim is built on Omniverse and is specialized for robotics simulation and policy testing. |
| 4 | What is the 'sim-to-real gap'? | Performance drop when a model trained in simulation meets real-world conditions (sensor noise, physics differences) not perfectly captured in simulation. Exam tip: a core challenge of Physical AI deployment. |
| 5 | What is the standard Physical AI decision loop? | Perceive (sensors) → Decide (model/control logic) → Act (actuators). Exam tip: perception must feed decision before any action occurs. |
| 6 | What is Omniverse primarily used for? | Building physically accurate, photorealistic 3D virtual worlds for simulation, digital twins, and collaborative content creation. Exam tip: foundation platform underlying Isaac Sim. |
| 7 | What is Isaac (Isaac Sim/Isaac ROS) used for? | NVIDIA's robotics-focused toolset for simulating, training, and testing robot perception and navigation before real-world deployment. Exam tip: robotics-specific, built atop Omniverse. |
| 8 | Why simulate robots before real-world deployment? | Simulation enables safe, scalable, repeatable testing across many randomized scenarios without the cost or risk of damaging real hardware. Exam tip: key justification for simulation's role in Physical AI. |
| 9 | Physical AI vs Generative AI — core distinction? | Physical AI perceives and acts in the real world (sensors + actuators). Generative AI creates digital content (text, image, audio) without physical embodiment. Exam tip: heavily tested distinction. |
| 10 | Common use cases for digital twins? | Predictive maintenance, real-time monitoring, and testing changes virtually before applying them to physical systems. Exam tip: digital twins are about live synchronization, not one-time simulation. |
| 11 | How does Physical AI connect to the broader NVIDIA stack? | Models are often trained/tested in simulation (Isaac/Omniverse), optimized (e.g., TensorRT), then deployed to edge hardware (e.g., Jetson) for real-world robotic action. Exam tip: shows end-to-end pipeline integration. |
| 12 | What technique helps close the sim-to-real gap? | Domain randomization — varying simulated conditions (lighting, textures, physics) during training so the model generalizes better to real-world variability. Exam tip: conceptual mitigation strategy, not a guaranteed fix. |
