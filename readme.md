
# Machine Learning for Efficient Substitution Control towards Azido Substituted L-Sugar Synthesis via Flow Chemistry

- rc-1.py represents the code for the selective azidation at C2 position of L-rhamnose for the synthesis of compound 2a.

- rc-2.py represents the code for the selective azidation at C2-C4 position of L-rhamnose for the synthesis of compound 2a'

- rc-3.py represents the code for the selective azidation at C2 position of L-fucose for the synthesis of compound 2b.

- rc-4.py represents the code for the selective azidation at C2-C4 position of L-fucose for the synthesis of compound 2b'.

## Enviorment setup for python 

To install all the required dependencies for running the Python program, first create and activate a virtual environment, then install the packages using the command below

```Bash
python -m venv flowopt-env
flowopt-env\Scripts\activate
pip install -r requirements.txt
```

## Hardware & System Connections

| Device                      | Port  | Baud Rate | Function               |
| --------------------------- | ----- | --------- | ---------------------- |
| HPLC Pump                   | COM30 | 9600      | Flowrate control       |
| Temperature Controller      | COM19 | 9600      | Heating and monitoring |
| Arduino Pressure Controller | COM52 | 9600      | Pressure regulation    |
| 3D Printer Collector        | COM6  | 115200    | Fraction collector     |

Ensure all COM ports are correctly assigned before running the code.

You can check available ports in device manager.

HPLC bought from KNAUER, Syringe pump, temperature and pressure controller has been bought from smart chem synthesis.

## Data Acquisition
Export FTIR spectral data to CSV format from ReactIR 15.

Update the path in the Python script:

mypath = r"C:\\Users\\Admin\\Desktop\\ruchi\\Exp 2024-09-17 10-34"

Ensure all instrument COM ports are correctly mapped.

Run the script (rc-1.py, rc-2.py, rc-3.py or rc-4.py) to start the closed-loop Bayesian optimization.

### The script:

- Runs the HPLC pump and sets the temperature and pressure.

- Monitors FTIR signals continuously.

- Integrates the area under the product-specific IR peak using:

- ```scipy.integrate.trapz```

- Uses this value as the objective function for Bayesian optimization.

- Saves each experiment’s conditions and corresponding IR area to CSV:

- ```output round <i>.csv```

## Model and Optimization

Algorithm: Bayesian Optimization using Gaussian Process (GP) surrogate

Kernel: Squared Exponential (RBF) with Automatic Relevance Determination

Acquisition Function: Expected Improvement (EI)

Implementation: skopt.Optimizer

### Search bounds:

- Flowrate: 1.0–10.0 mL·min⁻¹

- Temperature: 25–50 °C (rc-1.py) or 50–150 °C (rc-4.py)

- Pressure: 3–7 bar

- n_initial_points = 3 (Latin hypercube sampling)

- Maximum iterations = 22


