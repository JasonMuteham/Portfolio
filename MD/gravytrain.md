--- 

MP expenses are a *hot* topic in the UK, and the local MP raised eyebrows  with large claims for rented accommodation, even though they live in a constituency close to London. This made me wonder if the outrage was justified.
                  
The outcome? The Gravy Train. Now armed with data, the question is: How does your MP's spending compare?

<a href="https://gravytrain.streamlit.app" target="_blank" class="center-align"><img src="images/GravyTrain_Screenshot.png" ></a>

<a href="https://gravytrain.streamlit.app" target="_blank"><p>https://gravytrain.streamlit.app</p></a>

---

<h3 class="light-blue-text darken-1">The Gravy Train Data Stack</h3>

<a href="/gravytrain.html" target="_blank"><img src="images/EtL.png" class=""></a>

---

<h3 class="light-blue-text darken-1">The Gravy Train Pipeline</h3>

#### Data Sources
**UK Parliament**

The [UK Parliament](https://www.parliament.uk/) website hosts [Resources](https://developer.parliament.uk) for developers, including a directory of open data APIs which allow Parliamentary data to be shared publicly. All data is made available under the Open Parliament Licence. The following data is extracted.

* MP data.
* MP historic name data.
* Constituency details.
* Constituency historic representation data.
* Constituency geometry.

**IPSA**

The [Independent Parliamentary Standards Authority](https://www.theipsa.org.uk/), the independent body that regulates and administers the business costs and decides the pay and pensions of the 650 elected MPs and their staff in the UK. [Expense](https://www.theipsa.org.uk/mp-staffing-business-costs/annual-publications) claim data – released and updated every two months – includes details of all publishable claims for all MPs for a financial year. The following data is extracted. 

* All published expense claims 2010 - 2023, approx 2 million records.

#### Extract transform Load

There are many product options to extract from data sources and load into the database of your choice. After trying a few EtL open sources offerings, I decided to write my own parameter driven EtL process that will load to either **DuckDB** or **MotherDuck**, I call it  the **Quack Stack EtL Pipeline** the code is available on [GitHub](https://github.com/JasonMuteham/Quack_Stack_EtL_Pipeline).

Data is extracted from the sources and saved locally as CSV files. The CSV files are loaded into database using the Duckdb native CSV import functions. Although it is possible to load data in a similar manor to MotherDuck I found this to be unreliable (MotherDuck is still in development). I found the most reliable method is to create a local DuckDB database and use the MotherDuck extension to replicate the database in the cloud.

#### DBT


