<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Visualize data with QuickSight

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-analytics-quicksight)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-analytics-quicksight_6c7f7ef0)

---

## Introducing Today's Project!

We're here to upload a dataset to Amazon S3, connect it to Amazon QuickSight, analyze the data with charts and graphs, and publish a dashboard that showcases meaningful insights. It's all about turning raw data into a visual story!

### Tools and concepts

Services I used were Amazon S3 and Amazon QuickSight. Key concepts I learnt include storing datasets in the cloud using S3, configuring access through a manifest.json file, connecting and analyzing data in QuickSight, and creating and customizing visualizations and dashboards to uncover and present insights from the dataset.

### Project reflection

This project took me approximately 1 to 1.5 hours to complete. Most of the time went into setting up the S3 bucket and QuickSight connection, creating multiple visualizations, and refining the dashboard for presentation and export.

The next project I plan to do is building a CI/CD pipeline using AWS services like CodePipeline, CodeBuild, and CodeDeploy to automate application deployment. I plan to start it later this week, so I can continue expanding my skills in cloud development and DevOps.

---

## Upload project files into S3

The two files I stored in my S3 bucket are netflix_titles.csv and manifest.json.The netflix_titles.csv file is the dataset that contains information about Netflix shows and movies, such as titles, genres, release years, and countries. The manifest.json file is a configuration file that tells Amazon QuickSight where to find the dataset in S3 and how to interpret it for analysis.

I changed the S3 URL in the manifest.json file to point to the exact location of my netflix_titles.csv file in my S3 bucket. I edited this file so that Amazon QuickSight can correctly locate and access the dataset during the data import process. Without updating the URL, QuickSight wouldn’t know where the data is stored.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-analytics-quicksight_3c3cd85a)

---

## Create QuickSight account

Opening a QuickSight account does not cost money initially — Amazon offers a free trial of QuickSight (usually for 30 days) with access to many features. However, after the trial ends, charges may apply depending on the edition (Standard or Enterprise) and your usage. Always review the pricing and select the free trial option during sign-up to avoid unexpected charges.

Creating an account took me...It took me approximately 5 to 10 minutes to open a QuickSight account. The process involved signing in, selecting the correct edition, granting permissions, and setting up access to my S3 bucket.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-analytics-quicksight_f4ab4214)

---

## Download the Dataset

I visited the Datasets page in Amazon QuickSight to connect my S3 bucket. From there, I selected New dataset, chose S3 as the data source, entered the source name as kaggle-netflix-data, and pasted the S3 URL of my manifest.json file to establish the connection.

The manifest.json file was important in this step because it provided Amazon QuickSight with the exact location and structure of the dataset stored in S3. It allowed QuickSight to access the netflix_titles.csv file properly and understand how to load the data for visualization and analysis.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-analytics-quicksight_6f874996)

---

## My first visualization

To create visualizations on QuickSight, I selected a dataset, then dragged fields from the data pane into the visual editor—assigning them to axes, groupings, or values depending on the chart type. I explored different visual types like bar charts, donut charts, and tables, and customized each one by applying filters, sorting, and formatting to highlight insights clearly.

The visualization I uploaded shows a breakdown of Netflix titles by release year and content type (TV Show vs Movie). It helps visualize how Netflix's content offerings have changed over time—highlighting trends such as which years had more releases and whether TV shows or movies were more dominant in those periods.

I created this visualization by dragging the release_year field into the X Axis and the type field (TV Show or Movie) into the Group/Color section. This allowed me to display a stacked bar chart that shows the number and proportion of movies versus TV shows released each year, making it easy to compare content trends over time.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-analytics-quicksight_aff3aad7)

---

## Using filters

Filters are useful because they help you focus on specific parts of your data, making it easier to analyze patterns, answer targeted questions, and draw meaningful insights. Instead of viewing the entire dataset at once, filters allow you to narrow down the data based on certain conditions, like year, type, or country—helping you make your visualizations more relevant and clear.

ChatGPT said:
This visualization is a breakdown of the number of Netflix TV shows and movies added over time, grouped by release year and content type. Here I added a filter by country, so the chart only shows titles available in a specific region. This helps highlight how Netflix’s content offerings have evolved in that country over the years.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-analytics-quicksight_c32248c5)

---

## Setting up a dashboard

As a finishing touch before publishing my dashboard, I added clear, descriptive titles to each of my charts to make the insights easy to understand at a glance. Then I published the dashboard to share it with others and exported it as a PDF so I’d have a polished, shareable version of my work for documentation or presentation.

I exported my dashboard as a PDF by clicking the Export icon in the top right corner of the QuickSight dashboard, selecting Generate PDFs, and then waiting for the file to process. Once the green banner appeared confirming it was ready, I clicked Download to save the PDF version of my dashboard to my computer.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-analytics-quicksight_6c7f7ef0)

---

## Refreshing source data

---

---
