# pythonproject
import pandas as pd
import os

def read_dataframe_in_chunks_with_date_filter(file_directory, date_from, date_to, chunk_size=1000):
    while True:
        for file_name in os.listdir(file_directory):
            if date_from <= file_name <= date_to:
                # Construct the full file path
                file_path = os.path.join(file_directory, file_name)
                
                # Read the DataFrame in chunks
                for chunk in pd.read_csv(file_path, chunksize=chunk_size):
                    yield chunk  # Yield each chunk
                
        break  # Exit the loop after processing all files

# Example usage:
file_directory = '/path/to/your/directory'
date_from = '2023-01-01'
date_to = '2023-12-31'

for data_chunk in read_dataframe_in_chunks_with_date_filter(file_directory, date_from, date_to):
    # Process each chunk of data
    print(data_chunk.head())  # Replace with your processing logic
