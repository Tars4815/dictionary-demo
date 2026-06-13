# Contribution Guidelines

Thank you for helping us keep the Data Dictionary accurate and up-to-date! 

Good documentation is a team effort. You do not need to be a developer, know how to write code, or understand Git to contribute to this project. All content updates are managed through a simple spreadsheet.

---

## The Workflow

Updating the dictionary takes just three simple steps:

1. **Download the template:** Grab the latest version of the Data Dictionary Excel template from our shared team folder.
2. **Fill in the data:** Add or update the rows corresponding to the database tables and columns you are documenting.
3. **Submit for publishing:** Send the updated Excel file to the technical team. We will run an automated process to convert your spreadsheet into the web pages you see here.

---

## How to fill out the Excel template

Each sheet in the Excel file represents a single database table. For every column in that table, please provide the following details:

* **Column:** The exact technical name of the field in the database (e.g., `user_id`, `geom`, `created_at`).
* **Data type:** The format of the data (e.g., `VARCHAR(255)`, `UUID`, `POINT`, `INTEGER`).
* **Definition (IT) & Definition (EN):** A clear, business-friendly description of what the column represents. Please fill out both the Italian and English columns to support our bilingual platform.
* **Example value:** A realistic example of the data to help others understand the format (e.g., `john.doe@email.com` or `POINT(12.49 41.89)`).
* **Constraint?:** Note any database rules, such as `PK` (Primary Key), `FK` (Foreign Key), or `NOT NULL`.
* **Geometry?:** Specify if the field contains spatial data (e.g., `Yes - EPSG:4326` or `No`).
* **Comments (IT) & Comments (EN):** Any extra context, business logic, or warnings regarding how this data should be used or interpreted.

!!! warning "Keep Formatting Simple"
    Please avoid using complex Excel formatting like merged cells, custom cell colors, or multiple lines inside a single cell. Plain text ensures the smoothest conversion to the web platform!

---

## Submitting Your Changes

Once your Excel file is ready and reviewed:

* Upload the new version to the designated shared drive.
* Notify the database administration team via email or our internal chat.
* The team will process the file, and your changes will be live on the Data Dictionary within a few minutes!