# Two-Tone Experiment Workflow

This project defines a Two-Tone Experiment workflow using the Bonsai platform. It is an experimental framework for conducting behavioral neuroscience experiments, with functionalities for controlling hardware, generating stimuli, capturing responses, and logging data.

## Project Structure

- **TwoToneExperiment**: The main group workflow orchestrates the experiment sequence, managing trial initiation, stimulus presentation, joystick monitoring, and data logging.
- **Externalized Mappings**: Configurable parameters, such as response windows, inter-trial intervals (ITI), and thresholds, allow fine-tuning without modifying the core workflow.

## Workflow Components

### Experiment Control

1. **Trial Management**: 
   - `TrialDistribution` manages trial distribution with uniform random sampling for balanced trial types.
   - `Trial` increments each trial counter and records trial-related events and states.

2. **State Management**: 
   - `State` and `Trial` BehaviorSubjects hold current trial and experiment state.
   - `StateTransitions.csv` logs the state transitions during the experiment.

3. **Responses**:
   - **Joystick Input**: The workflow monitors joystick movements and compares them with defined thresholds (`Joystick Threshold` and `NoGo Threshold`). Responses are categorized as `Hit`, `Miss`, `FalseAlarm`, or `CorrectRejection`.
   - **Response Delay & Penalty**: Configurable delay penalties for early or incorrect responses can be set in the **Timeout Properties**.

4. **Sound Stimulus**:
   - **Go & NoGo Tones**: Defined tones (e.g., `RewardTone`, `MissTone`) play based on trial response type. The tones help subjects learn by associating specific sounds with outcomes.

### Data Logging and Output

- **CsvWriter Nodes**: 
  - `ResponseStat.csv`, `StateTransitions.csv`, and `sounds.csv` are log files generated to capture trial-by-trial data on responses, state changes, and auditory stimuli.
  
- **Response Statistics**: Real-time calculations and buffering of response statistics (e.g., correct/incorrect counts) are managed to provide cumulative data.

- **JoystickVisualizer**: Visualizes joystick movements relative to defined thresholds in a real-time graph. This feedback can help in understanding subject interaction.

### Hardware Integration

1. **Joystick Control**:
   - Joystick events (defined by thresholds for pull and movement) trigger specific responses and penalties.
   
2. **Harp Communication**: Configures the **Harp COM Ports** for hardware-based I/O communication, enabling joystick and sound card interfaces.

3. **Camera Control**: Although disabled by default, this includes options for camera capture and video recording, useful for recording experiment sessions.

### Visualizers

- **Response Stat Visualizer**: Displays response metrics throughout the experiment.
- **JoystickVisualizer**: Real-time graph for tracking joystick movement with `TrialGraph` showing values against thresholds.

## Externalized Parameters

Several experiment parameters are externalized, allowing for customization without editing the code directly:
  
- **Experiment Control**: `Number of Trials`, `Response Delay`, `Timeout Duration`, `Percentage Go Trials`, and `ITI Penalty`.
- **Tone Properties**: `RewardTone`, `MissTone`, `GoSound`, and `NoGoSound`.
- **Joystick Properties**: `Joystick Threshold`, `NoGo Threshold`, `ITI Upper Threshold`, and `ITI Lower Threshold`.
  
## How to Run

1. Configure necessary hardware connections (joystick and sound card via COM ports).
2. Adjust parameters in the externalized mappings to fit the experiment requirements.
3. Run the workflow in Bonsai to initiate the experiment.

## Notes

- This workflow is configured for flexibility, with components enabled or disabled as needed for specific setups.
- For advanced setups, additional workflows, such as **HarpJoystick** and **SoftSoundCard**, may be activated by removing their disabled state.

This workflow provides a robust foundation for running a Two-Tone Experiment with extensive logging, visualizations, and hardware support.
