

# Set Up a RAG Chatbot in Bedrock

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-bedrock)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Set Up a RAG Chatbot in Bedrock

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-bedrock_d5e8f1g2)

---

## Introducing Today's Project!

RAG (Retrieval Augmented Generation) is an AI technique that combines the power of a language model with a retrieval system. Instead of relying solely on pre-trained knowledge, RAG retrieves relevant information from an external data source—like your personal documents or a knowledge base—and uses that information to generate more accurate and context-specific responses.

In this project, I will demonstrate RAG by building a personalized chatbot using Amazon Bedrock, which accesses foundation AI models, and integrating it with Amazon S3 to store my documents and Amazon OpenSearch Serverless to index and search through them. This setup allows the chatbot to retrieve relevant content from my data in real time and generate responses that are tailored specifically to my information.

### Tools and concepts

Services I used were Amazon S3 for storing data, Bedrock for managing the AI model and processing data, and OpenSearch Serverless as the vector store to enable fast and accurate search. Key concepts I learnt include how to sync and embed data into a Knowledge Base, the importance of chunking and vectorizing text for semantic search, and how different AI models impact the quality of chatbot responses. I also gained experience troubleshooting AI models and understanding how to balance data retrieval with natural language generation.

### Project reflection

This project took me approximately a few hours to complete. The most challenging part was troubleshooting the AI model to ensure it provided accurate and relevant responses based on my Knowledge Base. It was most rewarding to see the chatbot generate personalized answers seamlessly, combining my data with its language understanding to create a truly interactive experience.

I did this project today to deepen my understanding of how AI-powered chatbots can be built and customized using real data, and to get hands-on experience with syncing, processing, and querying a Knowledge Base. Yes, this project met my goals by giving me practical insights into the entire workflow—from data ingestion to AI response generation—and helping me learn how to troubleshoot and improve chatbot performance effectively.

---

## Understanding Amazon Bedrock

Amazon Bedrock is a fully managed AWS service that provides access to foundation models from leading AI providers through an API, without needing to manage any infrastructure or machine learning expertise. It allows developers to build and scale generative AI applications securely and efficiently.

I'm using Bedrock in this project to create a RAG-enabled chatbot that can understand and respond using my own data. With Bedrock, I can easily integrate AI models with my documents stored in S3 and indexed via OpenSearch, allowing the chatbot to retrieve relevant information and generate accurate, personalized answers.

My Knowledge Base is connected to S3 because that’s where I store the documents containing the information I want my chatbot to use. S3 is a scalable object storage service on AWS, and it acts as the central location for uploading all my files—like PDFs, text documents, or notes—that the Knowledge Base will read and convert into searchable vectors.

By connecting the Knowledge Base to S3, Bedrock can automatically access, ingest, and index these documents so the chatbot can retrieve relevant content and provide meaningful responses based on the actual information I’ve uploaded.

In an S3 bucket, I uploaded documents that contain information about me—such as my background, skills, experiences, and any relevant notes or files I want my chatbot to learn from. These could be PDFs, text files, or markdown files that hold the knowledge the chatbot will use to answer questions.

My S3 bucket is in the same region as my Knowledge Base because Amazon Bedrock requires both resources to be in the same AWS region to ensure compatibility, reduce latency, and avoid cross-region data access issues.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-bedrock_b5c8d1e2)

---

## My Knowledge Base Setup

My Knowledge Base uses a vector store, which means it stores numerical representations (embeddings) of my documents to enable smart, meaning-based searches. When I query my Knowledge Base, OpenSearch Serverless will quickly search through these embeddings to find the most relevant chunks of information based on the meaning of my question—not just the keywords.

I'm using OpenSearch Serverless as my vector store because it's fully managed, scalable, and optimized for high-speed search and analytics. It allows Bedrock to retrieve accurate and contextually relevant results instantly, making my chatbot more intelligent and responsive.

Embeddings are numerical representations of text that capture the meaning, context, and themes of that text. They allow the AI to compare pieces of information based on similarity in meaning, rather than just matching exact words. When someone asks a question, embeddings help the chatbot find the most relevant parts of the documents—even if the wording is different—by comparing these number-based "meaning cards."

The embeddings model I'm using is Titan Text Embeddings v2 because it’s optimized for use within the AWS ecosystem. It's fast, accurate, and designed to work seamlessly with Amazon Bedrock, making it ideal for converting my Knowledge Base documents into searchable embeddings that power intelligent and context-aware responses.

Chunking is the process of breaking down large documents into smaller, manageable sections so that AI models can efficiently process and understand the content. Since models have a limit on how much text they can handle at one time, chunking ensures that the data is digestible and searchable without losing context.

In my Knowledge Base, chunks are set to 300 tokens by default, which is roughly equivalent to 300 words or punctuation marks. This helps the chatbot retrieve and respond with relevant sections of the document quickly and accurately.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-bedrock_p9r2s5t8)

---

## AI Models

AI models are important for my chatbot because they give it the ability to understand language, interpret questions, and generate human-like responses based on the information in my Knowledge Base. Without AI models, my chatbot would only be able to return static search results or keywords, rather than providing thoughtful, conversational answers.

These models—like the ones available in Amazon Bedrock—bring natural language understanding and generation capabilities, making the chatbot intelligent, interactive, and useful for answering questions in a personalized way.


To get access to AI models in Bedrock, I had to manually select the models I wanted to use and request access through the Bedrock console. This involved checking boxes next to the models—like Titan Text Embeddings V2, Llama 3.1 8B Instruct, and Llama 3.3 70B Instruct—and then submitting the request for AWS to review.

AWS needs explicit access because some models are more resource-intensive or come with usage policies that require approval. This process ensures users are making an intentional choice to use these models, helps AWS manage infrastructure capacity in specific regions, and allows providers like Anthropic or Meta to enforce their own terms of service.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-bedrock_model-access-proof)

---

## Syncing the Knowledge Base

Even though I already connected my S3 bucket when creating the Knowledge Base, I still need to sync because the content in the bucket may have changed since the initial connection—files might have been added, updated, or removed. Syncing ensures that the Knowledge Base has the most up-to-date information, enabling accurate and current responses based on the latest data stored in the bucket.


The sync process involves three steps: Bedrock first ingests the data by retrieving it from the connected source, such as an S3 bucket. Next, it processes the data by chunking it into smaller parts and embedding it—this means converting the text into numerical vectors that the model can understand. Finally, it stores the processed data in a vector store, like OpenSearch Serverless, allowing for fast and accurate retrieval when answering questions.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-bedrock_sync-screenshot)

---

## Testing My Chatbot

I initially tried to test my chatbot using Llama 3.1 8B as the AI model, but it struggled to provide accurate or detailed responses, especially when handling more complex or nuanced questions based on my data. I had to switch to Llama 3.3 70B because it offers significantly better reasoning, a deeper understanding of context, and more accurate retrieval capabilities—making it more reliable for generating high-quality, personalized answers from my Knowledge Base.

When I asked about topics unrelated to my data, my chatbot still responded confidently and accurately. This proves that it can fall back on its foundational language model knowledge to handle general queries, even when the information isn’t in the Knowledge Base. It shows that the chatbot can seamlessly blend retrieved data with general understanding to provide helpful answers.


You can also turn off the Generate Responses setting to limit the chatbot to only returning relevant documents from the Knowledge Base without generating a full natural language response. This is useful for debugging or when you want to verify exactly which pieces of data the model is retrieving. When you turn it back on, the chatbot uses those documents to generate complete, conversational answers.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-rag-bedrock_d5e8f1g2)

---

## Upgrading My Chatbot

---

---
