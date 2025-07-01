<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# How to Use DeepSeek

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-llm-deepseek)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-llm-deepseek_kkkkkkkk)

---

## Introducing Today's Project!

In this project, I will demonstrate how to explore and evaluate DeepSeek, one of the most advanced open-source Large Language Models available today. I'm doing this project to learn how DeepSeek compares to other LLMs like ChatGPT, how to run it locally using tools like Ollama and Chatbox, and how to customize it to suit my hardware and personal preferences. By testing prompts and reviewing performance, I’ll decide whether DeepSeek is a better fit for my AI projects going forward.

### Tools and concepts

Services I used were DeepSeek’s web app, Ollama for local model hosting, and Chatbox for an enhanced terminal chat interface. Key concepts I learnt include the importance of model size and parameter count in balancing performance and resource needs, how real-time reasoning (like DeepSeek R1’s “DeepThink”) improves answer accuracy, the benefits of hosting LLMs locally for privacy and offline use, and how adjusting the temperature setting can customize creativity versus precision in responses. After reviewing DeepSeek and OpenAI, I personally preferred DeepSeek for its transparent reasoning and accuracy in complex tasks, especially when running larger models locally—though ChatGPT’s speed and accessibility remain strong advantages.

### Project reflection

This project took me approximately 2 to 3 hours to complete. The most challenging part was setting up and running the larger DeepSeek models locally, especially managing system resources and waiting for responses with complex reasoning. It was most rewarding to see how the local hosting with Ollama and Chatbox gave me full control over the model’s behavior, including customizing temperature settings and witnessing DeepSeek’s transparent real-time reasoning in action.

I did this project today to deepen my understanding of emerging open-source Large Language Models and explore practical ways to run them locally for better privacy, control, and customization. I wanted to compare DeepSeek’s capabilities directly with established models like ChatGPT and see how advanced reasoning and settings like temperature affect performance. This project definitely met my goals—it gave me hands-on experience with installing, running, and tuning DeepSeek, and helped me appreciate the trade-offs between speed, accuracy, and creativity in different AI models.

---

## Exploring DeepSeek

DeepSeek is an open-source AI company that develops powerful Large Language Models (LLMs) designed to rival leading models like ChatGPT. Their R1 model gained attention for introducing a unique reasoning approach called "DeepThink," which allows the model to display its real-time thought process while generating responses. This includes intermediate steps such as questioning its own conclusions or verifying its logic—making the model more transparent and efficient. Unlike traditional models that simply predict the next word, R1 actively evaluates and improves its answers as it goes, resulting in more accurate and insightful outputs.

While you could access DeepSeek over the web app, some concerns are constant internet dependency, slower response times due to server load, and potential privacy risks since your data is processed on external servers. To address these concerns, I'm doing this step to install a tool called Ollama, which allows me to host DeepSeek locally on my own computer. This setup lets me use DeepSeek offline, ensures that all data stays private on my device, and speeds up interactions by eliminating reliance on external infrastructure.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-llm-deepseek_aaaaaaaa)

---

## Ollama and DeepSeek R1

Ollama is a tool that allows you to easily download, install, and run Large Language Models (LLMs) like DeepSeek directly on your own computer. It simplifies the complex process of setting up LLMs locally by handling all the backend tasks for you. With Ollama, you can interact with these models right from your terminal, giving you full offline access, enhanced privacy, and more control over how the models behave—such as adjusting parameters like temperature for different response styles.

You won't be able to find OpenAI models in Ollama because OpenAI’s models are not open-source—they are proprietary and confidential. This means the architecture, training data, and underlying code are not publicly available, so they cannot be downloaded or run locally. Ollama is designed to support open-source models like DeepSeek, which allow full access for local use and customization.

I tested using DeepSeek offline by turning off my computer’s WiFi and then entering a prompt, “Can I use DeepSeek while offline?” in the terminal. I observed that DeepSeek still generated a full response without any internet connection. You can also see ‘<think>’ tags in the terminal because they represent DeepSeek’s real-time reasoning process, showing how the model is actively thinking through the answer as it types—even when running entirely locally on my device. This offline capability is possible because the entire model runs on my computer without needing to send data to external servers.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-llm-deepseek_gggggggg)

---

## DeepSeek R1 Sizes

DeepSeek R1 has different model sizes, including 1.5b, 4b, and 8b versions. The model sizes are defined by the number of parameters, which means the tiny decision-making units inside the model that help it learn patterns from data and perform reasoning tasks. For example, the 1.5b model has 1.5 billion parameters. Generally, larger models with more parameters can handle more complex tasks and produce more accurate results, but they also require significantly more computing power and storage. Smaller models are faster and easier to run locally, making them good for quick tests or less demanding use cases.

The R1 model you choose to run locally depends on your computer’s available storage space and processing power. Having different model sizes helps with running R1 locally because smaller models like 1.5b require less memory and storage, making them accessible for most machines, while larger models like 7b or 8b offer more advanced reasoning and accuracy but need significantly more resources. This flexibility lets you pick the best balance between performance and hardware capability for your setup.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-llm-deepseek_iiiiiiii)

---

## Chatbox

To complete my local setup, I installed Chatbox to create a more user-friendly and organized interface for chatting with DeepSeek, similar to what a web app offers but running entirely on my computer. My Chatbox settings use the Ollama API as the model provider, connecting directly to the locally hosted DeepSeek model through the default API Host. This allows smooth communication between Chatbox and Ollama, letting me interact with DeepSeek in a visually appealing and efficient way.

I tested two different R1 model sizes, which were the 1.5b and 8b versions, using the prompt: "How many r's are in strawberry?" The results were that the 1.5b model gave an incorrect answer by counting only two r’s, likely due to its lighter architecture and limited reasoning ability. In contrast, the 8b model took longer to respond but provided the correct answer, demonstrating a deeper and more accurate chain of reasoning. This shows how larger models can better handle detailed analysis, even if they require more time and resources.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-llm-deepseek_kkkkkkkk)

---

## Temperature Settings

The temperature setting in an LLM determines how random or creative the model’s responses will be. A higher temperature makes the output more varied and unpredictable, encouraging creativity and exploration, while a lower temperature results in more focused, precise, and logical answers. To see this in action, I set the temperature to a high value like 2 in Chatbox using the DeepSeek R1 8b model, then asked, “What does the temperature setting do?” This helped me observe how the model’s explanation became more imaginative and diverse compared to lower temperature settings.

I started a third chat with ChatGPT to act as an impartial judge between the high and low temperature responses generated by DeepSeek. ChatGPT’s analysis will also help me understand the key differences in style, creativity, and logic between these two types of outputs, giving me insights into how temperature settings affect AI-generated text in a way that’s easy to interpret and evaluate.

ChatGPT quickly figured out which piece was generated with a high temperature, because the high-temperature response had a more creative, varied tone with richer vocabulary and less predictable phrasing. It showed more exploration and nuance in word choice, sometimes taking more imaginative or less conventional angles. In contrast, the low-temperature response was clearer, more focused, and precise, sticking closely to factual and straightforward language. This contrast made it easy for ChatGPT to distinguish the two styles and explain how temperature influences creativity versus accuracy in LLM outputs.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-llm-deepseek_aregearg)

---

## DeepSeek vs. OpenAI

I decided to compare DeepSeek R1 with OpenAI by using the prompt:

"Write a Python script for a bouncing yellow ball within a square. Make sure the square is slowly rotating. Make sure the ball stays within the square."

This is a challenging prompt because it combines multiple layers of complexity—real-time animation, mathematical transformations for a rotating shape, and accurate collision detection to keep the ball inside the moving boundaries. The model must not only understand how to animate objects in Python, but also apply geometric reasoning and physics to ensure the behavior of the ball is correct within the dynamically rotating square. This makes it a great test of each LLM's advanced reasoning and coding capabilities.

To test ChatGPT's response, I copied the generated Python script and ran it in Trinket to see the animation in action. ChatGPT's results were partially successful—the square was indeed rotating, which shows a solid understanding of transformation and animation logic. However, the script fell short in one key area: the bouncing ball inside the square was missing or not functioning correctly. This means the model handled the rotation requirement well but didn’t fully implement the logic needed for collision detection and ball movement within the rotating square. While quick and responsive, the solution lacked the complete integration of all prompt requirements.

Compared to ChatGPT's performance, I thought DeepSeek's response was more accurate and better aligned with the full complexity of the prompt. It delivered a complete solution with both the rotating square and the bouncing ball functioning correctly—showcasing strong reasoning and problem-solving abilities. I prioritize correctness and logical precision, especially for technical tasks like coding and simulations, so I preferred DeepSeek’s response despite the longer wait time. That said, ChatGPT’s speed and partial implementation were still impressive, making both models valuable depending on the task and priorities.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/ai-llm-deepseek_dfgbewrwq3)

---

## Token Efficiency

---
