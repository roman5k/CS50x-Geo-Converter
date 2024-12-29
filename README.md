# CS50x Geo Converter
#### Video Demo: [CS50x Final Project Geo Converter](https://youtu.be/xEKN9FiouOE)
#### Description:

This App is designed for people that want to convert coordinates to WGS84.

The user needs to register in order for him to utilize the conversion tool.

Once the user is signed in he can select or drag and drop one of the
3 file types csv, or xlsx, xlsm.

After connecting a file, you have to select the corresponding columns
regarding "Latitude" and "Longitude" which you want to convert to WGS84.

You also have to select the source coordinate system of the input coordinates.

By the time the necessary input fields are selected a preview will be shown
for the converted coordinates as well as where it would be on an OpenStreetMap.

By clicking the button 'Convert', the data is converted and the user will be
presented with a download popup. When this popup is cancelled, the user can
also utilize the newly added 'Download' button.

#### Installation:

1. **Clone the repository:**
    ```sh
    git clone https://github.com/roman5k/CS50x-Geo-Converter.git
    cd project
    ```

2. **Set up virtual environment:**
    ```sh
    python3 -m venv .venv
    source .venv/bin/activate
    ```

3. **Install the required packages:**
    ```sh
    pip install -r requirements.txt
    ```

4. **Run the application:**
    ```sh
    flask run
    ```

#### Routes:

- **`/`**: Home page
- **`/convert`**: Coordinate conversion page (requires login)
- **`/settings`**: User settings page (requires login)
- **`/change_password`**: Change password (requires login)
- **`/delete_account`**: Delete account (requires login)
- **`/login`**: User login page
- **`/logout`**: User logout
- **`/register`**: User registration page

#### Files/Folders:

1. **app.py**

    This file manages the backend of the app, so when the user wants to do
    something in the frontend a request is sent to the backend that handles
    the action the user intends to do and returns the output of the backend
    actions.

    In the routes `/change_password`, `/delete_account`, `/login`,
    `/logout`, `/register` the backend handles SQLite3 delete,
    validate, and change actions.

    The route `/convert` is the heart of the app.py file, because here the
    main feature of the app is handled appropriately. For the conversion
    of the input file by utilizing packages like pandas, pyproj, io and openpyxl.

    first the file is loaded and the active worksheet is initialized.
    with the selected longitude, latitude and source coordinate system
    columns the coordinates are converted to WGS84.

    **action `preview`**

    the first two converted coordinates are returned to the frontend for the
    user to verify the right selection of the source coordinate system.

    **action `convert`**

    with this action all the coordinates are updated in the excel file and
    then saved in order to provide the user for a download option with the
    same format as the input file.

2. **templates**

    **`/apology.html'**
    here the apology meme image generation api is used, so whenever there
    is an error or a faulty input, the user gets notified with this error
    message/page.

    **`/convert.html'**
    here the user can select a file via drag and drop or selection.
    once a file gets selected, the user will see additional dropdown
    fields for longitude, latitude and source coordinate system where
    longitude and latitude has the option of the column names in the
    source file. source coordiate system column offers two different
    choices for the source coordinate system to convert from.

    once the data is fully selected the preview coordinates as well as
    an openstreetmap is rendered in order to help the user if the result
    will be as expected.

    this functionality is handled by javascript, just like when the user
    presses convert, the data is send to the backend for the conversion
    to take place.

    **`/index.html'**
    this is the index or welcome page. depending on the logged in or not.
    the user will see slighty different buttons. this is handled by jinja
    condition in the html itself.

    **`/layout.html'**
    the layout handles the overall look of the frontend, especially the
    navigation bar and the footer link icon.

    **`/login.html'**
    this html page is for the login of the user with two input fields,
    one for the username and one for the password, and a login button.

    **`/register.html'**
    this html is for the registration of the user. it has two input fields,
    one for the username and two for the password, and a register button.
    we have two password fields for verifying that the user types the
    intended password.

    **`/settings.html'**
    in this html page, the user has two options. one is to change his password
    and the other is to delete his account.

3. **static**

    **`/style.css`**
    here additional style things are handled for the frontend pages.

    **`/pin.svg`**
    this is a pin icon that is used in the footer for a link to an external page
    on which u can check your coordinates for different coordiante systems.

3. **geo.db**

    this is the database that handles the user data such as hashed password and
    username.

4. **helpers.py**

    this file has two helper functions. one is used for making the login as a
    required condition. the other is to render the apology meme image.

