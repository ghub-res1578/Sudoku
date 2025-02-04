# Sudoku-Inspired Neural Network Simulation

## Overview
This repository contains a simulation of a **Sudoku-inspired threshold-coupled neural network** using **Brian2**, a neural simulation library. The model consists of 81 neurons arranged according to a valid Sudoku solution, with excitatory and inhibitory synaptic connections determined by the Sudoku structure.

## Simulation Details

### Neuron Model
The neurons are modeled with the following differential equation:

```
dv/dt = (I_d + I - v)/tau : 1
I = A*cos(2*pi*f*t) + 0.5 : 1
I_d : 1
```

where:
- `v` is the membrane potential
- `I` is an oscillatory input current with baseline offset
- `I_d` is a random drive current
- `tau` is the membrane time constant

### Network Structure
- **81 neurons** corresponding to Sudoku grid cells
- **Excitatory connections** within neurons sharing the same number
- **Inhibitory connections** for neurons within the same row, column, or subgrid

### Synaptic Connections
- **Excitatory synapses:** Connect neurons that share the same value in the Sudoku grid
- **Inhibitory synapses:** Connect neurons within the same row, column, or 3×3 subgrid

## Installation & Dependencies
Ensure you have the required Python packages installed:
```sh
pip install brian2 brian2tools numpy matplotlib tqdm
```

## Running the Simulation
To execute the simulation:
```python
python main.py
```

The script will:
1. Initialize the neuron group based on a Sudoku solution.
2. Construct the connectivity matrix based on the Sudoku structure.
3. Run a **30-second simulation** (real-time equivalent).
4. Save **spike train data**.

## Output Files
- **Spike Train Data**: Saved in `indi/spike_train_seedirandom_with_drive_in{seedi}_exc{exc}_inh{inh}.txt`
- **Plots**:
  - Neuron membrane potentials
  - Population firing rate over time

## Parameters
| Parameter | Description | Value |
|-----------|-------------|-------|
| `A` | Amplitude of input current | `-0.2` |
| `f` | Input oscillation frequency | `10 Hz` |
| `tau` | Membrane time constant | `40 ms` |
| `exc` | Excitatory synaptic weight | `0.002` |
| `inh` | Inhibitory synaptic weight | `0.006` |
| `seedi` | Random seed for reproducibility | `[3]` |

## Visualization
The script produces:
- **Membrane potential distributions** for all neurons
- **Population rate plots** using `brian_plot(rate_mon)`

## Future Work
- **Adjust synaptic plasticity mechanisms** for dynamic learning
- **Explore different Sudoku solutions** to analyze structural effects
- **Compare with real neuronal recordings** to investigate cognitive representations

