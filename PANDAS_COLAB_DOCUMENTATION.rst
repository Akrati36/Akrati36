.. _io.colab:

Loading Data in Google Colab
=============================

Google Colab provides several convenient ways to load data into pandas DataFrames.
This guide covers the most common methods for accessing data in the Colab environment.

.. contents:: Table of Contents
   :local:

From Local Files
----------------

Upload files directly from your computer using Colab's file upload widget.

.. code-block:: python

    from google.colab import files
    import pandas as pd
    import io

    # Upload file from your computer
    uploaded = files.upload()

    # Read CSV into DataFrame
    # Replace 'data.csv' with your filename
    df = pd.read_csv(io.BytesIO(uploaded['data.csv']))
    print(df.head())

.. code-block:: python

    # For Excel files
    df = pd.read_excel(io.BytesIO(uploaded['data.xlsx']))
    
    # For JSON files
    df = pd.read_json(io.BytesIO(uploaded['data.json']))

.. note::
   Uploaded files are stored in the Colab runtime and will be deleted when 
   the runtime disconnects. For persistent storage, use Google Drive.

From Google Drive
-----------------

Mount your Google Drive to access files stored in your Drive account.

.. code-block:: python

    from google.colab import drive
    import pandas as pd

    # Mount Google Drive
    drive.mount('/content/drive')

    # Read file from Drive
    df = pd.read_csv('/content/drive/MyDrive/data.csv')
    print(df.head())

.. code-block:: python

    # Access files in subdirectories
    df = pd.read_csv('/content/drive/MyDrive/Projects/DataAnalysis/data.csv')
    
    # Read Excel from Drive
    df = pd.read_excel('/content/drive/MyDrive/data.xlsx')

.. tip::
   Use Google Drive for:
   
   - Large files (>100MB)
   - Files you need across multiple sessions
   - Sharing data with collaborators

From URLs
---------

Load data directly from web URLs without downloading.

.. code-block:: python

    import pandas as pd

    # Read CSV from URL
    url = 'https://raw.githubusercontent.com/pandas-dev/pandas/main/doc/data/tips.csv'
    df = pd.read_csv(url)
    print(df.head())

.. code-block:: python

    # Read from any public URL
    url = 'https://example.com/data.csv'
    df = pd.read_csv(url)
    
    # Read Excel from URL
    url = 'https://example.com/data.xlsx'
    df = pd.read_excel(url)
    
    # Read JSON from URL
    url = 'https://api.example.com/data.json'
    df = pd.read_json(url)

From GitHub
-----------

Access data files stored in GitHub repositories.

.. code-block:: python

    import pandas as pd

    # Use raw.githubusercontent.com URL
    github_url = 'https://raw.githubusercontent.com/username/repository/main/data.csv'
    df = pd.read_csv(github_url)
    print(df.head())

.. code-block:: python

    # Example with pandas repository
    url = 'https://raw.githubusercontent.com/pandas-dev/pandas/main/doc/data/air_quality_no2.csv'
    df = pd.read_csv(url)

.. note::
   To get the raw URL from GitHub:
   
   1. Navigate to the file on GitHub
   2. Click the "Raw" button
   3. Copy the URL from your browser

From Kaggle Datasets
--------------------

Download and load datasets from Kaggle using the Kaggle API.

.. code-block:: python

    # Install kaggle package
    !pip install kaggle

    # Upload your kaggle.json API credentials
    from google.colab import files
    uploaded = files.upload()  # Select your kaggle.json file

    # Set up Kaggle credentials
    !mkdir -p ~/.kaggle
    !mv kaggle.json ~/.kaggle/
    !chmod 600 ~/.kaggle/kaggle.json

    # Download dataset
    !kaggle datasets download -d username/dataset-name

    # Unzip the dataset
    !unzip dataset-name.zip

    # Load into pandas
    import pandas as pd
    df = pd.read_csv('data.csv')
    print(df.head())

.. tip::
   Get your Kaggle API credentials:
   
   1. Go to https://www.kaggle.com/
   2. Click on your profile picture → Account
   3. Scroll to "API" section
   4. Click "Create New API Token"
   5. Download kaggle.json

From Google Sheets
------------------

Load data directly from Google Sheets.

.. code-block:: python

    import pandas as pd

    # Make sure the sheet is shared (Anyone with link can view)
    sheet_url = 'https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit#gid=0'
    
    # Convert to CSV export URL
    csv_url = sheet_url.replace('/edit#gid=', '/export?format=csv&gid=')
    
    # Read into DataFrame
    df = pd.read_csv(csv_url)
    print(df.head())

.. code-block:: python

    # Alternative: Using gspread library
    !pip install gspread

    from google.colab import auth
    import gspread
    from google.auth import default
    import pandas as pd

    # Authenticate
    auth.authenticate_user()
    creds, _ = default()
    gc = gspread.authorize(creds)

    # Open spreadsheet
    spreadsheet = gc.open('Spreadsheet Name')
    worksheet = spreadsheet.sheet1

    # Get all values and convert to DataFrame
    data = worksheet.get_all_values()
    df = pd.DataFrame(data[1:], columns=data[0])
    print(df.head())

From SQL Databases
------------------

Connect to SQL databases and load data into pandas.

.. code-block:: python

    import pandas as pd
    from sqlalchemy import create_engine

    # SQLite example
    engine = create_engine('sqlite:///database.db')
    df = pd.read_sql('SELECT * FROM table_name', engine)
    print(df.head())

.. code-block:: python

    # PostgreSQL example
    !pip install psycopg2-binary

    engine = create_engine('postgresql://user:password@host:port/database')
    df = pd.read_sql('SELECT * FROM table_name', engine)

.. code-block:: python

    # MySQL example
    !pip install pymysql

    engine = create_engine('mysql+pymysql://user:password@host:port/database')
    df = pd.read_sql('SELECT * FROM table_name', engine)

Best Practices
--------------

File Size Considerations
~~~~~~~~~~~~~~~~~~~~~~~~

- **Small files (<10MB)**: Use direct upload or URLs
- **Medium files (10-100MB)**: Use Google Drive
- **Large files (>100MB)**: Use Google Drive or cloud storage with streaming

Data Persistence
~~~~~~~~~~~~~~~~

- Uploaded files are **temporary** and deleted when runtime disconnects
- Use **Google Drive** for persistent storage
- Save processed data back to Drive for future use

.. code-block:: python

    # Save DataFrame to Google Drive
    df.to_csv('/content/drive/MyDrive/processed_data.csv', index=False)

Security
~~~~~~~~

- Never commit API keys or credentials to notebooks
- Use environment variables or Colab secrets for sensitive data
- Be cautious when sharing notebooks with uploaded data

Performance Tips
~~~~~~~~~~~~~~~~

- For large files, use ``chunksize`` parameter in ``read_csv``
- Consider using ``usecols`` to load only needed columns
- Use ``dtype`` parameter to optimize memory usage

.. code-block:: python

    # Read large file in chunks
    chunk_size = 10000
    chunks = []
    for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
        # Process each chunk
        chunks.append(chunk)
    df = pd.concat(chunks, ignore_index=True)

Common Issues and Solutions
---------------------------

File Not Found Error
~~~~~~~~~~~~~~~~~~~~

**Problem**: ``FileNotFoundError: [Errno 2] No such file or directory``

**Solutions**:

1. Check file path is correct
2. Ensure Google Drive is mounted (if using Drive)
3. Verify file was uploaded successfully
4. Use absolute paths instead of relative paths

.. code-block:: python

    # Check current directory
    !pwd
    
    # List files in current directory
    !ls
    
    # List files in Drive
    !ls /content/drive/MyDrive/

Permission Denied Error
~~~~~~~~~~~~~~~~~~~~~~~

**Problem**: ``PermissionError: [Errno 13] Permission denied``

**Solutions**:

1. Check file permissions in Google Drive
2. Ensure Drive is mounted with correct permissions
3. Verify you have access to the shared file/folder

.. code-block:: python

    # Remount Drive with full permissions
    from google.colab import drive
    drive.mount('/content/drive', force_remount=True)

Upload Timeout
~~~~~~~~~~~~~~

**Problem**: File upload times out or fails

**Solutions**:

1. Use Google Drive for large files instead of upload
2. Check internet connection
3. Try uploading smaller batches
4. Use URL loading if file is available online

Memory Error
~~~~~~~~~~~~

**Problem**: ``MemoryError`` when loading large files

**Solutions**:

1. Use ``chunksize`` parameter to read in chunks
2. Use ``usecols`` to load only needed columns
3. Optimize dtypes to reduce memory usage
4. Upgrade to Colab Pro for more RAM

.. code-block:: python

    # Load only specific columns
    df = pd.read_csv('large_file.csv', usecols=['col1', 'col2', 'col3'])
    
    # Optimize dtypes
    df = pd.read_csv('file.csv', dtype={'col1': 'int32', 'col2': 'float32'})

See Also
--------

* :ref:`io.read_csv` - Read CSV files
* :ref:`io.read_excel` - Read Excel files
* :ref:`io.read_sql` - Read SQL databases
* :ref:`io.read_json` - Read JSON files
* :ref:`io.read_html` - Read HTML tables

External Resources
------------------

* `Google Colab Documentation <https://colab.research.google.com/>`_
* `Kaggle API Documentation <https://github.com/Kaggle/kaggle-api>`_
* `Google Drive API <https://developers.google.com/drive>`_