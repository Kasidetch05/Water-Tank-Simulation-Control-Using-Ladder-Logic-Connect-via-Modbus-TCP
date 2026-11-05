# Water-Tank-Simulation-Control-Using-Ladder-Logic-Connect-via-Modbus-TCP

My first PLC project. A ladder logic program keeps a water tank between 20% and 85% full.
A small Python program acts as the real tank, so you can test everything without hardware.

---

OpenPLC Runtime (Docker) <--- Modbus TCP, port 5020 ---> Tank Simulator (Python)
---

# How it works

1. Press **START** to turn the system on. Press **STOP** to turn it off.
2. When the water drops below the low switch (20%), the **pump** turns on.
3. The pump keeps running until the water reaches the high switch (85%).
4. At 85% the pump turns off and the **full lamp** lights up.

## Inputs and outputs

| PLC address | Tag          | What it is                    |
|-------------|--------------|-------------------------------|
| %IX0.0      | START_BUTTON | Start push button             |
| %IX0.1      | STOP_BUTTON  | Stop push button              |
| %IX0.2      | LOW_LEVEL    | TRUE when water is above 20%  |
| %IX0.3      | HIGH_LEVEL   | TRUE when water reaches 85%   |
| %QX0.0      | PUMP         | Pump                          |
| %QX0.1      | FULL_LAMP    | Tank full lamp                |

## Folders

- `WaterTank/` – OpenPLC Editor project (ladder logic is in `pous/programs/main.ld`)
- `TankSimulator/` – the virtual tank (Python)


## What you need

- OpenPLC Editor 4.3.3 or newer
- Docker Desktop (runs OpenPLC Runtime v4)
- Python 3

## How to run

1. Open Docker Desktop, then start the OpenPLC Runtime:
   ```
   docker run -d --name openplc-runtime -p 8443:8443 --cap-add=SYS_NICE --cap-add=SYS_RESOURCE -v openplc-runtime-data:/var/run/runtime ghcr.io/autonomy-logic/openplc-runtime:latest
   ```
   Next time,  just run `docker start openplc-runtime`.

2. Double-click `TankSimulator/Start Tank.bat`. The tank window opens.
3. Open the `WaterTank` folder in OpenPLC Editor. Click **Build and upload**, then **▶ Start PLC**.
4. Press **START** in the tank window. "PLC link" turns green and the tank starts to fill.

**Try it:** Move the outflow valve slider, or click **Drain to 10%**, and watch the pump turn back on.
> **Note:** Keep the project in a folder path with English letters only (for example `C:\PLC Project`).
> OpenPLC can fail to build from other paths.

   


