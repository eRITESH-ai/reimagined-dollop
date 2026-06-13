# Dynamic Event-Driven Control for BioDevices

This project explores dynamic event-driven control for regulating the pH of a simulated biological device. The goal is to demonstrate how event-driven control can significantly reduce computational load and energy consumption while maintaining tracking accuracy comparable to continuous or time-triggered approaches.

## Project Overview

Continuous control in resource-constrained environments (like biomedical implants) is often inefficient. This project proposes and evaluates a dynamic event-driven control mechanism where the controller updates only when a significant 'event' (deviation from desired state) occurs, rather than at fixed time intervals.

## Core Components

The simulation involves:

1.  **`BioDevice` (The Plant Model)**: Simulates a biological system (e.g., a proton pump) affecting pH, incorporating decay, control inputs, and noise.

2.  **`DynamicTrigger` (Event-Driven Innovation)**: Implements a dynamic event-triggering mechanism based on an internal 'patience' variable (`gamma`) and a cost function (`C`). It activates the controller only when a threshold is crossed, signaling a need for an update.

3.  **Control Strategies**: The `simulate_and_compare` function evaluates three paradigms:
    *   **Continuous Control**: Updates every simulation step (baseline).
    *   **Time-Triggered Control**: Updates at fixed time intervals (e.g., every 5 steps).
    *   **Event-Driven Control**: Updates only when `DynamicTrigger` signals an event.

## Key Findings

Dynamic event-driven control significantly reduces resource usage while maintaining or improving tracking accuracy. 

With 1000 total time steps:
*   **Continuous Updates**: 1000
*   **Time-triggered Updates**: 200
*   **Event-driven Updates**: 9

### Resource Impact

| Method         | Normalized Energy per Run (Baseline = 1.0) | Relative Battery Life Gain (× Baseline) | Number of Control Updates |
| :------------- | :----------------------------------------- | :-------------------------------------- | :------------------------ |
| Continuous     | 1.0000                                     | 1.0×                                    | 1000                      |
| Time-triggered | 0.2000                                     | 5.0×                                    | 200                       |
| Event-driven   | 0.0090                                     | 111.1×                                  | 9                         |

This shows a **99.1% reduction in control updates** and a **~111-fold increase in estimated battery life** for event-driven control compared to continuous. Tracking performance remains comparable, demonstrating efficiency without sacrificing accuracy.

## How to Run

1.  **Prerequisites**: Install `numpy` and `matplotlib`.
    ```bash
    pip install numpy matplotlib
    ```
2.  **Code**: The simulation code is within a single Python script or notebook cell.
3.  **Execution**: Run the script. The `simulate_and_compare()` function will execute the simulation, print results, and display plots.
    ```python
    # Assuming the code is in 'event_driven_control.py'
    python event_driven_control.py
    ```

## Visualizations

Plots generated include:

*   **pH Tracking Comparison**: pH level over time for all three methods.
*   **Tracking Error Comparison**: Absolute error from target pH over time.
*   **Resource Impact Plots**: Bar charts comparing energy, battery life, and processing load.
