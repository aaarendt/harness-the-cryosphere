## EC2 deployment

- **Instance type:** start with `m6i.2xlarge` (8 vCPU, 32 GB RAM, ~$0.38/hr on-demand). Prioritizes compile speed + RAM over GPU, since the local models in use (`qwen3.5:2b`, `qwen3.5:4b`) are small and CPU inference is fine for now.
  - Leaner budget alternative: `c6i.xlarge` (4 vCPU, 8 GB RAM, ~$0.17/hr).
  - Only move to a GPU instance (`g5.xlarge` or `g6.xlarge`, ~$1.00/hr) if/when specifically benchmarking local GPU inference.
- **AMI:** Ubuntu 22.04 or 24.04 LTS — plain Linux, not WSL2. Removes a layer of environment quirks.
- **Storage:** 100 GB gp3 EBS volume (model weights + cargo registry + build artifacts add up).
- **Security group:** SSH (22) restricted to my IP only. No other open ports.
- **Cost control:** stop (don't terminate) the instance when not in use — billed only while running; EBS storage persists between sessions.
- **Access:** VS Code Remote-SSH, so the workflow looks identical to local dev.

**Important caveat:** OpenJarvis's evaluation framework treats energy as a joint first-class metric alongside accuracy/cost/latency, using real hardware power monitoring (NVIDIA/AMD/Apple). A cloud VM can't measure wall-power draw the same way, so **energy-aware evals need to stay on local hardware** even after the main dev environment moves to EC2.
