## 🚀 RISC-V SoC Design and Tapeout Program — VSD
## Week 0: Foundation & Toolchain Setup
---
## Overview: Getting Started

In this first week, I’ve laid the groundwork for designing a System-on-Chip (SoC) with RISC-V. This includes installing all the essential open-source tools and walking through the digital VLSI flow from specification to preparatory steps for the physical design.

---

## Introduction

Welcome to Week 0 of my journey into RISC-V SoC design! My goals this week:

- Outline the complete digital VLSI flow—from behavior models to final layout preparation.  
- Install and test open-source EDA tools needed for RTL simulation, waveform analysis, layout, and verification.  
- Document what works, what needs attention, and establish reproducible setup steps.

---

## Digital VLSI Flow 

I’m following this sequence of development phases:

| Phase | Description |
|---|---|
| **Specification** | Define what the SoC should do; usually a behavior model in C or equivalent. |
| **RTL Development** | Write the hardware logic in Verilog / SystemVerilog. |
| **Synthesis & Netlist** | Turn RTL into gate-level netlist. |
| **Physical Design Preparation** | Floorplanning, placement, routing, and preparing GDSII masking steps. |
| **Verification & Checks** | Ensure each intermediate artifact matches intended behavior (functional & equivalence checking). |
| **Tapeout** | Run DRC/LVS,ship to foundry. |
| **Tapein** | Fabricate,dice and package. |
---

## Core Philosophy

A few guiding principles I’m following:

- *Consistency across abstraction levels:* Behavior as modeled initially must match behavior after synthesis, layout, etc.  
- *Verification at every stage:* Not pushing forward until tests pass.  
- *Clear modular breakdown:* Isolate core from peripherals, separate tools for simulation, layout, etc., so problems are easier to trace.

---

## Tool Setup & Installation

**Platform**: Ubuntu 22.04 (or your similar Linux distro)  
**Hardware**: ~4 CPU cores, ~6+ GB RAM, adequate storage (~50-70 GB)  

Here are the tools I got installed:

- Yosys (for RTL synthesis)  
- Icarus Verilog (for simulation)  
- GTKWave (waveform viewing)  
- NgSpice (for SPICE or analog-mixed signal checks)  
- Magic (layout viewer / simple DRC)  
- OpenLane (RTL-to-GDSII flow)  

### Tool Installation Workflow

## Yosys
```
sudo apt update
sudo apt install -y build-essential clang bison flex libreadline-dev \
     gawk tcl-dev libffi-dev git zlib1g-dev libboost-system-dev libboost-filesystem-dev \
     python3
git clone https://github.com/YosysHQ/yosys.git
cd yosys
make config-gcc
make
sudo make install
```
# Check
```
yosys --version
```
##Icarus Verilog
```
sudo apt-get update
sudo apt-get install iverilog
iverilog -V
```
## GTKWave
```
sudo apt-get update
sudo apt-get install gtkwave
gtkwave --version
```
##NgSpice
```
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release && cd release
../configure --with-x --with-readline=yes --disable-debug
make
sudo make install
```
## Check
```
ngspice --version
```
## Magic
```
sudo apt-get install m4 tcsh csh libx11-dev \
tcl-dev tk-dev libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
sudo make install
magic -d XR
```
## OpenLANE
```
sudo apt-get update && sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o \
/usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot
docker run hello-world
```
## 🛠️ Progress Summary

| Tool           | Purpose                           | Status               |
|----------------|-----------------------------------|----------------------|
| **Yosys**      | RTL → Gate-level synthesis        | ✅ Installed & tested |
| **Icarus Verilog** | Simulation & testbench verification | ✅ Working           |
| **GTKWave**    | Debugging waveforms               | ✅ Installed          |
| **NgSpice**    | Analog / mixed-signal simulation  | ✅ Built & running    |
| **Magic**      | Layout / basic DRC checks         | ✅ Installed          |
| **OpenLane**   | Full RTL → GDSII physical design  | ⚙️ Setup ongoing      |
Maintained by K Kavya
