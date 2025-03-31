# Polaris Subnet

## Subnet Purpose and Objectives

**Polaris** is a Bittensor subnet designed as a decentralized GPU compute marketplace and management layer. Its primary goal is to **connect miners who have spare GPU resources with the Bittensor network**, enabling those GPUs to be used for AI tasks and other compute-intensive workloads in a trustless environment.

Polaris's **mission** is to be *"the best place on this planet to list your GPUs,"* simplifying how operators join the Bittensor compute network. To achieve this, Polaris offers user-friendly tools to register and manage compute nodes across distributed environments.

Key objectives of the Polaris subnet include:

- **Decentralized Compute Market:** Create a trustless marketplace for GPU compute resources
- **Robust Validation:** Ensure reliable and accurate performance measurement
- **Ease of Use and Management:** Provide intuitive tools for node operators
- **Seamless Bittensor Integration:** Maintain compatibility with the Bittensor ecosystem

## Technical Requirements

Running a Polaris node (either as a miner or validator) requires meeting certain hardware, software, and network prerequisites. Below are the minimum and recommended requirements to ensure stable operation:

### Hardware Requirements

- **Operating System:** A Linux environment is required to run Polaris. Native installation on Ubuntu 20.04/22.04 (or other Debian-based distributions) is recommended. Windows 10/11 users can participate via WSL2, and macOS users can run a Linux VM or use Docker.
- **CPU & RAM:** 
  - 64-bit multi-core processor (Intel/AMD) with 2-4+ cores
  - Miners: Minimum 8GB RAM (16GB recommended)
  - Validators: Similar CPU/RAM requirements
- **GPU (Mining Nodes Only):**
  - Minimum: NVIDIA GPU with ~4GB VRAM (e.g., GTX 1660/RTX 2060)
  - Recommended: High-performance GPUs (RTX 3090/4090, A100/H100)
  - Multiple GPUs supported
- **Storage:** 
  - Minimum: 2GB free space
  - Recommended: 50+ GB for workloads/datasets
  - SSD recommended for better performance
- **Network:**
  - Reliable internet connection
  - 5+ Mbps upload/download (10+ Mbps recommended)
  - Public IP address or proper port forwarding
  - Ports: 8000 (API) and 11000-11002 (SSH)

### Software Requirements

- **Python:** Version 3.8+ (3.10 recommended)
- **Docker:** For containerized environments
- **Git:** For repository management
- **OpenSSH Server:** For secure connections
- **NVIDIA Drivers:** Latest version for your GPU
- **NVIDIA Container Toolkit:** For Docker GPU support

**Note on GPUs and Drivers:** Polaris itself does not impose specific GPU model requirements, but the **better the GPU, the higher the potential rewards**. Modern NVIDIA GPUs (Turing architecture or newer) have proven effective on Bittensor's compute tasks. Ensure you have the latest NVIDIA drivers installed and disable power-saving modes for optimal performance.

## Competitiveness Guidance

### Performance Measurement

In the Polaris subnet, **miners' performance is evaluated by validators** using various metrics:
- GPU capability (model and CUDA cores)
- Number of GPUs
- Available VRAM
- Network bandwidth
- Actual computational throughput

**Higher-performance miners will earn higher scores and greater rewards**, as the Bittensor consensus rewards contributions proportionally to their value.

### Staying Competitive

To remain competitive as a **miner** on Polaris:

- **Use High-Performance Hardware:** Invest in quality GPUs and maintain optimal performance
- **Maintain Excellent Uptime:** Keep your node running consistently
- **Optimize Network Settings:** Ensure stable connectivity and proper port forwarding
- **Stay Updated:** Keep your Polaris installation current with `polaris update subnet`
- **Monitor Performance:** Use built-in tools like `polaris monitor` and `polaris logs`
- **No Custom Model Training Needed:** Polaris focuses on raw compute power, not AI model quality

For **validators**, competitiveness focuses on:
- Continuous availability
- Accurate performance measurement
- Reliable hardware for handling multiple connections
- Professional operation mindset
- Regular software updates

## Installation Instructions

### Miner Installation

1. **Prepare the System:**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io git openssh-server python3.10 python3-pip
```

2. **Clone the Repository:**
```bash
git clone https://github.com/bigideaafrica/polaris.git
cd polaris
```

3. **Run the Installation Script:**
```bash
chmod +x polaris_manager.sh
./polaris_manager.sh
```

4. **Follow the Interactive Setup:**
   - Choose "Install Polaris"
   - System will check requirements
   - Set up Python virtual environment
   - Configure network settings
   - Initialize Polaris environment

5. **Register Your Node:**
```bash
polaris register
```
   - Choose "Bittensor Miner Node"
   - Create or use existing wallet
   - Select network (Mainnet netuid 49 or Testnet netuid 100)

6. **Start Mining:**
```bash
polaris start
```

### Validator Installation

1. **Create Wallets:**
```bash
pip install bittensor-cli==9.1.0
btcli wallet new_coldkey --wallet.name <your_wallet_name>
btcli wallet new_hotkey --wallet.name <your_wallet_name> --wallet.hotkey default
```

2. **Register Keys:**
```bash
btcli subnet register --netuid 49 --subtensor.network finney --wallet.name <your_wallet_name> --wallet.hotkey default
```

3. **Verify Registration:**
```bash
btcli wallet overview --wallet.name <your_wallet_name> --subtensor.network finney
```

4. **Run Validator:**
```bash
docker pull bateesa/polaris-validator
docker run --rm -it -v ~/.bittensor:/root/.bittensor -e WALLET_NAME=<your_wallet_name> -e WALLET_HOTKEY=default bateesa/polaris-validator
```

## Usage

### Common Commands

- `polaris start` - Start Polaris services
- `polaris stop` - Stop Polaris services
- `polaris status` - Check service status
- `polaris logs` - View service logs
- `polaris monitor` - View real-time metrics
- `polaris update subnet` - Update to latest version
- `polaris --help` - Show all available commands

### Monitoring and Management

- Use `polaris monitor` for real-time performance tracking
- Check logs with `polaris logs` for troubleshooting
- Monitor system resources and GPU usage
- Keep software updated with `polaris update subnet`

## FAQ

### General Questions

**Q: Do I need an AI model or to train anything to mine on Polaris?**
A: No – Polaris is a compute-focused subnet. You provide raw computing power (GPU cycles) rather than serving a machine learning model. Hardware performance is key, not AI model quality.

**Q: What kind of rewards will I earn?**
A: Miners earn TAO tokens based on their performance. Rewards are distributed through the Bittensor network's consensus mechanism.

**Q: What is the difference between a miner and a validator?**
A: Miners provide GPU compute resources, while validators verify miner performance and maintain network consensus. Most participants will be miners.

### Technical Questions

**Q: Can I use an existing Bittensor wallet?**
A: Yes, you can use an existing wallet, but some users may need to regenerate or re-import wallets specifically for Polaris.

**Q: Can I run multiple Polaris miners?**
A: Yes, you can run multiple instances to utilize multiple GPUs or machines. Each instance can use the same or different wallets.

**Q: Is there a testnet available?**
A: Yes, you can use the Testnet (netuid 100) for experimentation without using real TAO tokens.

### Troubleshooting

**Q: My miner isn't getting rewards or tasks. How do I know it's working?**
A: Check `polaris status` and `polaris logs` for activity. Verify your ports are open and your public IP is correctly configured.

**Q: My node fails to start or crashes. What can I do?**
A: Check logs, ensure correct Python version, verify wallet configuration, and consider reinstalling if needed.

## Support and Resources

- Official Polaris documentation
- Bittensor community forums and Discord
- GitHub Discussions and Issues
- Community channels for hardware and provider recommendations

## License

This project is licensed under the MIT License. You are free to use, modify, and distribute Polaris's code in accordance with the MIT terms.

---

*Polaris Subnet is an open-source initiative by Big Idea Africa, aiming to democratize access to AI compute. By participating in Polaris, you're contributing to a more decentralized and accessible future for AI development. Happy mining!* 🚀
