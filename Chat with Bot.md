<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Chat With Your Bot in the Terminal

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-cloudshell)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Interacting With My RAG Chatbot in the Terminal

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-cloudshell_1i2j3k4l)

---

## Introducing Today's Project!

In this project, I will set up a chatbot by first storing the information it needs to know in an S3 bucket, then creating a Bedrock Knowledge Base to help the chatbot understand that information. Next, I will select AI models in Bedrock to enable the chatbot to communicate effectively what it has learned. Finally, I will interact with the chatbot through the terminal using AWS CloudShell. I’m doing this project to learn how to build, configure, and test an AI-powered chatbot that can provide personalized responses based on my own data.

### Tools and concepts

The services I used were Amazon S3 to store my chatbot's data, Amazon Bedrock to create and manage the Knowledge Base, and AWS CloudShell to run CLI commands and interact with the chatbot. The key concepts I learnt included how to build a Retrieval-Augmented Generation (RAG) chatbot, the process of ingesting, processing, and embedding data into a vector store, syncing the Knowledge Base, selecting and using AI models, and using the AWS CLI to test and refine chatbot interactions.

### Project reflection

This project took me approximately a few hours to complete. The most challenging part was configuring the Bedrock command correctly with the required parameters like the Knowledge Base ID and Model ARN. It was most rewarding to see the chatbot successfully generate accurate, personalized responses using the data I uploaded, proving that all the components were working together as expected.

I did this project today to get hands-on experience with building a Retrieval-Augmented Generation (RAG) chatbot using Amazon Bedrock and other AWS services. I wanted to understand how to connect data sources, configure AI models, and interact with a chatbot through the CLI. Yes, this project met my goals—it helped me learn how to create a functional, personalized chatbot from scratch and gave me practical insights into syncing data, embedding content, and troubleshooting AI responses.

---

## Setting Up The Knowledge Base

To set up my Knowledge Base, I used S3 to securely store and organize all the documents and data that my chatbot will learn from. The documents I uploaded contain information about the topics and knowledge I want the chatbot to understand and reference when answering questions, ensuring that the chatbot’s responses are accurate and relevant to my specific content.

I also created a Knowledge Base in Bedrock to organize and process the information stored in my S3 bucket, enabling the AI models to effectively understand and search through the data. This helps the chatbot retrieve relevant information quickly and generate accurate, context-aware responses based on the content I provided.


My chatbot also needs access to two AI models, which were Titan Text Embeddings V2 and Llama 3.3 70B Instruct. I then synchronized my Knowledge Base to ensure that the latest data from my S3 bucket was ingested, processed, and stored properly so the AI models could accurately understand and use this information when generating responses. Synchronizing keeps the Knowledge Base up to date with any new or changed content.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-cloudshell_1u2v3w4x)

---

## Running CLI Commands in CloudShell

AWS CLI is a command-line tool that allows me to interact with AWS services by typing commands instead of using the web console. To start testing CLI commands, I first opened CloudShell, which is a browser-based terminal provided by AWS that comes pre-configured with the AWS CLI and other tools, making it easy to run commands without any local setup.

When I first ran a Bedrock command, I ran into an error because I needed to provide values for parameters such as the Knowledge Base ID, the AI model name, and the user query. These values are essential for the command to know which Knowledge Base to search, which model to use for generating responses, and what question to answer.

While finding the parameters takes extra time, the advantage of using the CLI is that it provides a powerful and flexible way to interact directly with AWS services and tools, automate repetitive tasks, and quickly test or troubleshoot without needing a graphical interface. It’s especially useful for developers and engineers who want precise control and the ability to script complex workflows.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-cloudshell_sdrgsert)

---

## Running Bedrock Commands

To find the required values, I had to navigate to the Amazon Bedrock console and copy the Knowledge Base ID and the Model ARN for the AI model I selected. The Bedrock command ran successfully and showed me a response from the chatbot based on the information stored in my Knowledge Base, confirming that the setup and integration were working correctly.

The retrieve-and-generate command typically also outputs a lot of additional metadata along with the chatbot’s answer, which can make the terminal response harder to read. To tidy up the terminal response, I added the --query parameter to filter the output and display only the chatbot's generated response, making it much easier to focus on the actual answer.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-cloudshell_1i2j3k4l)

---

## Extending Your Knowledge Base

---

## Interacting with AI Models Directly

---

---
