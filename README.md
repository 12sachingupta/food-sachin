

#

1. Process a single CSV file:

   ```bash
   python spoiltracker.py --csv_file data.csv --production_date 2023-06-01
   ```

2. Generate an expiry report based on existing history data on products expiring in 7 days:

   ```bash
   python spoiltracker.py --days 7
   ```

3. Clear expired entries and the expiry report:

   ```bash
   python spoiltracker.py --clear-expired
   ```

4. Batch process files in a directory:

   ```bash
   python spoiltracker.py --batch ./examples/batch/
   ```

5. Output a pretty-printed expiry report for products expiring within 10 days:

   ```bash
   python spoiltracker.py --table --days 10
   ```

## Method Descriptions

The SpoilTracker package provides the following methods in the `ExpiryTracker` Class:

- `load_shelf_life_data()`: Loads the shelf life data from the shelf life file.
- `calculate_expiration_date(production_date, shelf_life)`: Calculates the expiration date based on the production date and shelf life.
- `append_to_history(data)`: Appends data to the history file.
- `append_to_expiry_report(data, days, output_dest=None)`: Appends data to the expiry report file for products that fall within the specified threshold.
- `sort_expiry_report(output_dest)`: Sorts the expiry report file by expiration date.
- `generate_expiry_report(days, output_dest=None)`: Generates the expiry report for products that fall within the specified threshold.
- `clear_expired_entries()`: Removes expired entries from the history file and clears the expiry report file.
- `clear_history_file()`: Clears the history file.
- `process_csv(csv_file_path, prod_date)`: Processes a CSV file, calculates expiration dates, and returns the processed data.
- `print_table(output_dest=None, show_console=False)`: Prints a pretty-formatted table of the expiry report and saves it as a text file.
- `run(csv_file=None, production_date=None, days=3, clear_expired=False, output_dest=None, clear_history=False, print_table=False)`: Runs the SpoilTracker functionality based on the provided arguments.

### Python Script Integration

To use Spoiltracker in a Python script, you can import the `ExpiryTracker` class and create an instance of it. Then, call the `run` method with the desired parameters.

```python
from spoiltracker import ExpiryTracker

expiry_tracker = ExpiryTracker()
expiry_tracker.run(csv_file="sku_list.csv", production_date="2023-06-01", days=5, remove_expired=True)
```

## How To Customize

Spoiltracker requires shelf life data to calculate expiration dates. You can load youre own csv file of SKUs, products, and their shelf life and keep track of daily production. By default, it expects a CSV file named "shelflife.csv" in the `./csv` directory. The file should have the following columns: SKU, Name, Brand, "Shelf Life" (in days).

```csv
SKU,Name,Brand,Shelf Life
123,Product 1,Brand 1,10
456,Product 2,Brand 2,7
```

You can customize the shelf life file path by providing it when creating an instance of `ExpiryTracker`.

```python
expiry_tracker = ExpiryTracker(shelf_life_file="custom_shelflife.csv")
```

## Dependencies

SpoilTracker has the following dependencies:

- `argparse`: For parsing command-line arguments.
- `csv`: For reading and writing CSV files.
- `os`: For working with file paths and directories.
- `datetime`, `timedelta`: For working with dates and calculating expiration dates.
- `tabulate`: For generating formatted tables.

## License

See [MIT License](/LICENSE).

## Contributing

See [Contributing Guidelines](/CONTRIBUTING).


