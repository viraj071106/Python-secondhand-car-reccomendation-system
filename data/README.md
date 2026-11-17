# Dataset location

Put the CSV exported from the Kaggle kernel here as:

```text
data/car_dataset.csv
```

The training script accepts common second-hand-car column names such as
`price`, `selling_price`, `year`, `mileage`, `km_driven`, `fuel`, `brand`,
`model`, `transmission`, `owner`, and `engine`. It prints the detected mapping
and fails clearly if no usable target or numeric feature can be found.

The command supplied in the request can be used after installing and
authenticating the Kaggle CLI:

```bash
kaggle kernels pull ceydalgz/car-dataset -p data/kaggle_kernel
```

If that command produces a notebook rather than a CSV, export its dataset to
`data/car_dataset.csv` before training.
