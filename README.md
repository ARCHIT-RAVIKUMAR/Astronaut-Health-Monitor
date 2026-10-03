# Astronaut Health Monitor

A web dashboard that monitors the health status of one astronaut (Archit Ravikumar) during a simulated mission. All readings are randomly generated and change every 2 seconds.

**Live link:** https://archit-ravikumar.github.io/Astronaut-Health-Monitor/

## Features

- Five parameters: heart rate, oxygen saturation (SpO2), body temperature, sleep duration, exercise time
- Status for each parameter and overall: Normal, Warning or Critical
- Mission elapsed time (day and time) and last-reading time
- Alert banner and a running alert log
- Demo buttons to trigger low oxygen, high heart rate and fever

## How the data works

There is no backend. A JavaScript loop generates a new reading every 2 seconds, and each update represents 5 minutes of mission time. Heart rate and temperature follow the astronaut's activity (sleep, rest, exercise) with random noise. Oxygen stays near 98% with occasional random dips. Sleep is set once per mission day, and exercise minutes build up during two daily workout windows.

## Alert condition and logic

Each reading is compared against fixed thresholds:

| Parameter | Normal | Warning | Critical |
|---|---|---|---|
| Heart rate (rest) | 50-100 bpm | 100-120 or 40-50 | above 120 or below 40 |
| Heart rate (exercise) | up to 150 | 150-170 | above 170 |
| Oxygen (SpO2) | 95% or higher | 90-94% | below 90% |
| Body temperature | 36.0-37.5 C | 37.6-38.4 or 35.5-35.9 | 38.5 or above, or below 35.5 |
| Sleep (last night) | 6 h or more | 4.5-6 h | below 4.5 h |
| Exercise (goal 120 min) | on track | under 60 min after 20:00 | none |

The main alert is oxygen below 90%, which shows a red CRITICAL ALERT banner and adds an entry to the log. The overall status is the worst level among all parameters. There is also a combined rule: SpO2 under 94% together with a resting heart rate above 100 bpm gives a warning for possible respiratory distress. Alerts are logged when a status gets worse and again when it returns to normal, so the log does not repeat on every update.

Note: this is a demo with simulated data, not a medical tool.
