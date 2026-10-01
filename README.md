# LMU Telemetry Analytics

LMU Telemetry Analytics is a local-first project for analysing Le Mans Ultimate
session telemetry. It is intended for drivers who want to review their sessions
and compare laps after driving.

## What It Will Provide

- Comparison between two laps over the full circuit.
- Time delta and segment analysis.
- Speed, throttle, brake, and other telemetry traces when the data is available
  and validated.
- Identification of sections where one lap gains or loses time against another.
- Session history, lap consistency, stint analysis, and performance tracking in
  later product increments.

## How It Will Work

The project will read a recorded LMU session, preserve the original source,
process the available telemetry, and present the resulting lap analysis locally.

The first version will compare eligible laps by track distance. A later local web
interface is planned for selecting sessions and laps and viewing charts. A circuit
map depends on validated spatial telemetry or a reliable source of track geometry.
