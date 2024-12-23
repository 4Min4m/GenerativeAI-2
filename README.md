In this module, you will watch a demonstration of running the notebooks that support the knowledge base discussion presented in the previous module. If you have access to an AWS account, you can use the instructions provided to run the notebooks in your account.

By the end of this demo, you should be able to do the following:

Leverage a fully-managed RAG application with Amazon Bedrock RetrieveAndGenerate API.

Build a Q&A application using Amazon Bedrock Knowledge Bases with Retrieve API.

Test the Query Reformulation process supported by Amazon Bedrock Knowledge Bases.

Build and evaluate Q&A Application using Amazon Bedrock Knowledge Bases using RAG Assessment (RAGAS) framework.

Test the guardrail functionality on Amazon Bedrock Knowledge Base using RetrieveAndGenerate API.

The demo lab tasks are as follows:

Task 0: Set up the environment. For this task, you run the Task-0.ipynb notebook file.

Task1: Leverage a fully-managed RAG application with Amazon Bedrock's RetrieveAndGenerate API. For this task, you run the Task-1.ipynb notebook file.

Task 2: Build a Q&A application using Amazon Bedrock Knowledge Bases with Retrieve API. For this task, you run the Task-2.ipynb notebook file.

Task 3: Test the Query Reformulation process supported by Amazon Bedrock Knowledge Bases. For this task, you run the Task-3.ipynb notebook file.

Task 4: Build and evaluate Q&A Application using Amazon Bedrock Knowledge Bases using RAG Assessment (RAGAS) framework. For this task, you run the Task-4.ipynb notebook file.

Task 5: Test the guardrail functionality on Amazon Bedrock Knowledge Base using RetrieveAndGenerate API. For this task, you run the Task-5.ipynb notebook file.

Getting started

The lab task notebook files are provided below. You can use these if you have access to an AWS account. Download each file to your local computer, saving them all in the same folder.




In addition, there are also six image files that are required by the notebooks. In the folder that you saved the notebook files, create a folder called images, and download and save these files in there.



Finally, there is a document that you will use for a RAG task. In the folder that you saved the notebook files, create a folder called KB file, and download and save this file in there.


Setting up the lab environment in your AWS account

In order to run these demo lab tasks, you will need to request access to the necessary Amazon Bedrock models, then launch Amazon SageMaker to access and set up the Jupyter Labs environment. Finally, you will upload the the task notebook files to the lab environment. Run the Task0 notebook and follow the directions in this notebook to install all of the packages that you need to run Tasks 1 through 5.

Note: for maximum compatability, use Google Chrome for your web browser.

Setup demonstration video

The provided directions will walk you through the steps necessary to set up your environment to conduct the labs if you have access to an AWS account. Follow the directions to complete the steps. This video will demonstrate the process.

To start the lab set up demonstration, choose the play button. A transcript follows the video.


In this lab, you build a question-answering application using the AnyCompany knowledge base and Amazon Bedrock's Retrieve and RetrieveAndGenerate API. You leverage the existing knowledge base, which contains comprehensive information about AnyCompany's products, services, corporate details like history, leadership, financial performance, sustainability efforts, and more. You run through various notebooks that can effectively answer questions related to AnyCompany's products, services, and corporate information.

In this first task, you will set up your lab environment so you can complete these labs. This will require you to request model access in Amazon Bedrock as well as set up your lab environment in Amazon SageMaker Studio.

To begin, you will need to download the Jupyter notebook files that you will need to compete the labs. There are 6 notebook files total, as well as 1 PDF file and 6 image files that will be required for some of the labs.

Once you have downloaded the files to your local computer, note the location. You will need to access the contents to run these labs.

To use Bedrock, account users with the correct IAM Permissions must enable access to available Bedrock foundation models (FMs). In order to select the models you will need, make sure you are in the us-east-1 region.

At the top of the AWS Management Console, in the search bar, search for and choose Amazon Bedrock.

Go to the Amazon Bedrock console page. Choose Get Started.

If you see a welcome popup, select Manage model access. Otherwise, use the navigation menu on the left side and scroll down to Model access.

To add to or update your existing model access, choose Enable specific models.

On the Edit model access page, locate the following models and use the checkboxes to select them if you do not already have access to them:

Titan Embeddings G1 – Text

Titan Text G1 - Premier

Then scroll down.

Note: If you notice that the access status already shows Access granted, no action is required. If you do not see Titan Text G1 – Premier as one of the options, make sure you are in the us-east-1 region.

Finally, find Claude 3 Sonnet. Verify that it is selected, and if it is not, use the checkbox to select it.

Then scroll down.

Once you have verified that all the models are selected or already available, choose Next.

Review your selections, if applicable, then choose Submit.

Once your access has been granted, you will now be able to use these models with the lab notebooks.

In this step, you will set up and review the knowledge base that you will be using with the Jupyter lab notebook files.

To start, choose S3 from the favorites bar. If you don't have a favorites bar, enter it in the search bar and choose it from the list of services.

Choose create bucket.

Enter a unique name for your RAG bucket, then scroll down.

Leave everything else as default, and choose Create bucket.

The RAG S3 bucket has been successfully created.

Upload the financial document into the folder set up for RAG. Choose Upload.

To select the document, choose Add files.

Choose the AnyCompany_financial_10K.pdf file from the lab files that you downloaded and extracted earlier.

To finish, choose Upload.

Your file has been successfully uploaded.

In the search field, enter Amazon Bedrock.

Choose Amazon Bedrock from the list of services.

Choose Get Started.

Choose Knowledge bases from the navigation menu.

To get started, choose Create knowledge base.

Under Knowledge base name, enter e2e-rag-knowledgebase.

Under IAM permissions, make sure Create and use a new service role is selected. Keep the default name, then scroll down.

Make sure Amazon S3 is selected under Choose data source.

Leave everything else as default and choose Next.

For the Data source name, enter e2e-rag-knowledgebase-ds.

Next, choose Browse S3 to select the bucket you just created.

Select the bucket you created in S3 that contains the file for RAG.

Leave everything else as default and choose Next.

Under Embeddings model, choose Titan Embeddings G1 – Text v1.2, then scroll down.

Leave everything else as default and choose Next.

Review the details of the knowledge base as you scroll down to bottom of the page.

To finish, choose Create knowledge base.

Your vector database is being prepared in Amazon Opensearch Serverless.

The knowledge base has been successfully created. The banner provides a reminder that the next step is to sync the data source. Choose the Go to data sources button in the banner.

With your Data source selected, choose the Sync button.

The status shows the source is syncing. Wait for it to show as available.

The sync is complete. Now it's time to set up Amazon SageMaker.

In this step, you will launch an Amazon SageMaker Studio application to access your lab environment.

At the top of the AWS Management Console, in the search bar, search for and choose Amazon SageMaker.

To proceed, you will need to set up a domain. Select Set up for single user.

You will see a Preparing SageMaker Domain banner. This is a one time configuration and will take several minutes.

Now you need to set role permissions. First, scroll down to Authentication and permissions.

Take note of the Default Execution role, you will need to make updates to the permissions for this role.

Now you need to set role permissions. Use the 3 bars to expand the navigation menu.

Select Role manager from the navigation menu.

Since you are working with an established role, choose View roles in IAM manager.

Choose the link for the role you just created.

To get started, choose Add permissions, then choose Create inline policy.

In the Select a service search bar, Enter and choose Bedrock, then choose Next.

Expand the List section. Choose List Guardrails and List Knowledge Bases.

Expand the Read section. Choose ApplyGuardrail, InvokeModel, and Retrieve.

Expand the Write section. Choose CreateGuardrail and Retrieve and Generate, then scroll down.

Expand the Tagging section. Choose TagResource in this section.

Finally, under Resources, choose All. Then choose Next.

Use the Policy name field to give your policy a name, then select Create policy.

Your permissions policy has been added and is in effect.

Switch back to the tab with Amazon Sagemaker. Choose Domains from the navigation menu, select the current domain, and then choose the User Profiles tab.

Choose Launch button next to the user profile that was created, then select Studio.

Once you are in Studio, you may see a tour popup. Choose Skip Tour for now.

Once you are in Studio, under Applications, choose the JuypterLab button.

Select the Create JupyterLab space button.

Give your lab space a name and then choose Create Space.

Once the Lab Space is created, choose the Run Space button. The Status will change to Starting.

Once the status changes to Running, choose the Open JupyterLab button to launch Studio in a new tab.

In this step, you will prepare your lab resources. This includes uploading notebook files and running updates to the lab environment before you begin your tasks.

Once JupyterLabs opens, you will be working with the root folder. This is where you will upload files and create folders.

Use the New Folder icon and create a folder called images. Open this folder.

Choose the Upload icon to upload the image files needed for this lab.

Select all the image files for this lab from the Images folder from the files that you extracted. Once you've selected them all, choose Open to upload the files.

The images have been uploaded to the corresponding folder.

Return to the root folder.

Choose the Upload icon to upload the notebook files needed for this lab.

Select all the notebook files for this lab from the files that you extracted. Once you've selected them all, choose Open to upload the files.

You should see all the task files uploaded to your lab environment.

To finalize the Task setup, you will need to run Task-0. Open the Task-0 notebook file.

Run the code cell by using the Run button. This will install and update everything you will need to run these labs. After running the code cell, make sure you restart the kernel before continuing.

Congratulations! Your environment is setup, and you are ready to continue.

You have successfully done the following:

Requested access to Amazon Bedrock models.

Created and synched your knowledge base.

Launched and configured Amazon SageMaker.

Uploaded setup files for the labs.

Updated the kernel and files in the environment.

Task demonstration walkthrough

The provided directions will walk you through the steps necessary to run the labs, as well as provide a walkthrough of each task.

To start the demonstration, choose the play button. A transcript follows the video.

In this lab, you build a question-answering application using the AnyCompany knowledge base and Amazon Bedrock's RetrieveAndGenerate API. You leverage the existing knowledge base, which contains comprehensive information about AnyCompany's products, services, corporate details like history, leadership, financial performance, sustainability efforts, and more. You run through various notebooks that can effectively answer questions related to AnyCompany's products, services, and corporate information.

By the end of this lab, you should be able to do the following:

• Leverage a fully-managed RAG application with Amazon Bedrock RetrieveAndGenerate API.

• Build a Q and A application using Amazon Bedrock Knowledge Bases with Retrieve API.

• Test the Query Reformulation process supported by Amazon Bedrock Knowledge Bases.

• Build and evaluate a Q and A Application using Amazon Bedrock Knowledge Bases using RAG Assessment (or RAGAS) framework.

• Test the guardrail functionality on Amazon Bedrock Knowledge Base using RetrieveAndGenerate API.

In this first task, you leverage a fully-managed Retrieval Augmented Generation (or RAG) application with Amazon Bedrock's RetrieveAndGenerate API. For this task, you run the Task-1.ipynb notebook file.

Review the initial information provided for Task 1, which is separated into subtasks.

Examine the final lab architecture.

In Task 1.1, run the first code cell to initialize the boto3 client and setup your environment.

Run the next code cell to verify the ID for the existing Knowledge Base in Amazon Bedrock.

The cell output is displayed in the notebook. The knowledge base ID is provided for verification.

In Task 1.2, you test the Knowledge Base using the retrieve and generate function.

You initially test the knowledge base using the RetrieveAndGenerate API. With this API, Amazon Bedrock takes care of retrieving the necessary references from the knowledge base and generates the final answer using a foundation model (or FM) from Amazon Bedrock.

Run the following two code cells to initiate a query for testing the knowledge base. The first cell creates the query.

The next cell uses the query to test the knowledge base.

The output here is a summary of consolidated statements of cash flows for AnyCompany Financial for the fiscal year ended December 31, 2019.

In Task 1.3, you will understand the RetrieveAndGenerate API in detail.

Run the following two code cells for stating the default prompt for the knowledge base. The first cell states the default knowledge base prompt.

The second cell defines the retrieve and generate parameters.

In Task 1.4, you leverage the maximum number of results feature. In some use cases, the responses from the FM might lack enough context to provide relevant answers or rely that it could not find the requested information. This can be fixed by modifying the maximum number of retrieved results.

In this task, you run the following query using one result:

Provide a list of risks for AnyCompany financial in bulleted points.

Run the following two code cells. The first cell defines print generation results.

Then run the second cell, which contains the query and will output the results.

A list of the key risks for AnyCompany Financial mentioned in the search results is generated.

In the next code box, max results has been changed from one to three.

Run the code cell with the modified value for number of retrieved results.

The generated response is a list that is double the length of the previous one, with more identified risks.

As you can see from the output, by modifying the number of retrieved results to three, you get more results leading to a much more comprehensive response.

In Task 1.5, you customize the default prompt with your own prompt based on the use case. This feature helps adding more context to the FM which requires specific output format, languages and other contexts.

You use the PromptTemplate class from Langchain to parametrize the custom prompt template. You use the output format variable to modify the output at run time.

Run this code cell to create a helper function that supports customizing the template.

For Task 1.5.1, you use the same query example and default the FM to output to a different language.

Run the following three code cells to test an example that provides an output in French. The first cell provides the prompt.

The second cell requests that the response is provided in French.

Here you can see the combined output of the first two cells.

The third cell will provide the results of the search in the language specified, which is French.

A list of the key risks for AnyCompany Financial is generated, in French, as requested.

Finally, in Task 1.5.2, you use the same query example and default the FM to output in JSON format.

Run the code cell to test an example that provides an output in JSON format.

The response is a list that is generated in JSON format.

You have completed this notebook. Close this notebook file and continue with Task 2.

In Task 2, you build a Q and A application using Amazon Bedrock Knowledge Bases with Retrieve API. Here, you query the knowledge base to get the desired number of document chunks based on similarity search. You then augment the prompt with relevant documents and perform a query which acts as input to Anthropic Claude for generating response.

Review the initial information provided for the task, including the scenario.

Review the initial information provided for the task. In Task 2.1, you initiate the Amazon Bedrock client and perform the following operations:

- Verify the Knowledge Base ID.

- Import the necessary libraries and set up the necessary clients

In Task 2.1.1, you verify the Knowledge Base ID.

To run this notebook, you need to verify and assign the Knowledge Base ID to the kb ID variable and install the required packages.

Run the code cell to verify the ID for the existing Knowledge Base in Amazon Bedrock.

The knowledge base ID is provided and can be verified.

In Task 2.1.2, you initiate the Amazon Bedrock client.

Run the code cell to import the necessary libraries for setting up your environment.

The region is provided for verification to show the environment is set up correctly.

In Task 2.2, you define a retrieve function that calls the Retrieve API provided by the Knowledge Base for Amazon Bedrock which converts user queries into embeddings, searches the knowledge base, and returns the relevant results, giving you more control to build custom workflows on top of the semantic search results.

Review the initial information provided for the task.

Run the code cell to define a retrieve function that calls the Retrieve API.

In Task 2.2.1, you initialize your Knowledge Base ID before querying responses from the initialized LLM. You call the Retrieve API, and pass the Knowledge Base ID, number of results and query as parameters.

Run the following code cell to call the Retrieve API by passing the Knowledge Base ID, number of results and query as parameters.

You can view the associated score of each of the text chunk that was returned, which depicts its correlation to the query in terms of how closely it matches it.

In Task 2.2.2, you extract the text chunks from the Retrieve API response.

Run the following two code cells to fetch the context from the retrieval results and print them.

The first code box fetches the context from the response.

This second cell prints the context results.

Here are the results.

All the chunks have been extracted from the text.

In Task 2.2.3, you use a specific prompt for the model to act as a financial advisor AI system that provides answers to questions by using fact based and statistical information when possible. You provide the Retrieve API responses from earlier task as a part of the {contexts} in the prompt for the model to refer to, along with the user query.

Run the code cell to use a specific prompt for the model to act as a financial advisor AI system.

In Task 2.2.4, you invoke a foundation model from Amazon Bedrock.

Run the following two code cells to invoke the anthropic.claude-3-sonnet-20240229-v1:0 foundation model from Amazon Bedrock.

You are passing both the context and the query to the model. Run the second cell.

The response text is provided as output.

Task 2.3 involves LangChain integration.

In this task, you build a Q and A application using the AmazonKnowledgeBasesRetriever class from LangChain. You query the knowledge base to get the desired number of document chunks based on similarity search. Following that you integrate it with LangChain chain to pass the document chunks and the query to the LLM (which is Anthropic Claude 3 Sonnet) for answering questions.

In Task 2.3.1, you set up your environment. Run the code cell to import the necessary packages for setting up your environment.

In Task 2.3.2, you create a AmazonKnowledgeBasesRetriever object from LangChain which calls the Retrieve API provided by Amazon Bedrock Knowledge Bases. This converts user queries into embeddings, searches the knowledge base, and returns the relevant results, giving you more control to build custom workflows on top of the semantic search results.

Run the code cell to create the AmazonKnowledgeBasesRetriever object.

The results are presented for you.

In Task 2.3.3, you use specific prompt for the model to act as a financial advisor AI system that provides answers to questions by using fact based and statistical information when possible. You provide the Retrieve API responses from above as a part of the {context} in the prompt for the model to refer to, along with the user query.

Run the code cell to use a specific prompt for the model to act as a financial advisor AI system.

Finally, in Task 2.3.4, you integrate the retriever and the LLM using Langchain Expression Language (or LCEL) to build the Q and A application.

The response is provided as an output.

You have completed this notebook. Close this notebook file and continue with Task 3.

In Task 3, you understand and test the Query Reformulation process supported by Amazon Bedrock Knowledge Bases. With query reformulation, you take a complex input prompt and break it down into multiple sub-queries. These sub-queries separately go through their own retrieval steps for relevant chunks. The resulting chunks are then pooled and ranked together before passing them to the Foundational Model to generate a response. Query reformulation is another tool that helps in increasing the accuracy for complex queries that your application may face in production.

In this first task, Task 3.1, you setup the notebook environment by import the necessary packages.

Run the following two code cells to import the necessary packages and setup your environment.

After running the first cell, the boto3 version is provided as output.

Run the second cell.

The region and account ID are provided as output.

Run the code cell to verify the ID for the existing Knowledge Base in Amazon Bedrock.

The knowledge base ID has been provided for verification.

Run the code cell to define the FM to be used for this notebook.

In Task 3.2, you demonstrate query reformulation. You investigate a simple and a more complex query that could benefit from query reformulation and see how it affects the generated responses.

In Task 3.2.1, you see how the generated result looks like for the following query without using query reformulation. You use the following query: Where is the AnyCompany company waterfront building located and how does the whistleblower scandal hurt the company and its image?

Run the following three code cells to generated results without query reformulation. The first one creates the query.

The second code box will print the response when run.

The output is provided for you.

Run the third cell to examine the chunks that generate the response.

The number of citations or chunks used to generate the response is provided, along with the chunk, location, and metadata.

As seen from the above citations, your retrieval with the complex query did not return any chunks relevant to the building, instead focusing on embeddings that was most similar to the whistleblower incident.

This may indicate the embedding of the query resulted in some dilution of the semantics of that part of the query.

In Task 3.2.2, you see how query reformulation can benefit the more aligned context retrieval, which in turn, will enhance the accuracy of response generation.

Run the two code cells to generated results with query reformulation.

The first cell provides the response as a generated text output.

Run the next cell to take a look at the retrieved chunks with query reformulation.

As you can see, with query reformulation turned on, the chunks that have been retrieved now provide context for the whistleblower scandal and the location of the waterfront property components.

You have completed this notebook. Close this notebook file and continue with Task 4.

In this next task, you build and evaluate a Q and A application using Retrieve API provide by Amazon Bedrock Knowledge Bases, along with LangChain and RAGAS for evaluating the responses. Here, you query the knowledge base to get the desired number of document chunks based on similarity search, prompt the query using Anthropic Claude, and then evaluate the responses effectively using evaluation metrics, such as faithfulness, answer relevancy, context recall, context precision, context entity recall, answer similarity, answer correctness, harmfulness, maliciousness, coherence, correctness and conciseness.

In Task 4, you use AnyCompany's financial 10k reports (a synthetically generated dataset) as a text corpus to perform Q and A on. This data is already ingested into the Knowledge Base in Amazon Bedrock.

Review the initial information provided for the task.

In Task 4.1, you set up the environment

To run this notebook, you need to install dependencies, LangChain and RAGAS and updated boto3, botocore packages.

Run the first code cell to verify the ID for the existing Knowledge Base in Amazon Bedrock.

The knowledge base ID is provided as an output for verification.

Run the next code cell to install dependencies.

In Task 4.2, you create a AmazonKnowledgeBasesRetriever object from LangChain to search the knowledge base and return the relevant results, giving you more control to build custom workflows on top of the semantic search results.

Run the code cell to create a AmazonKnowledgeBasesRetriever object.

In Task 4.3, you invoke the model and visualize the response using the following information:

Question: Provide a list of few risks for AnyCompany financial in numbered list without description."

Ground truth answer

1. Commodity Prices

2. Foreign Exchange Rates

3. Equity Prices

4. Credit Risk

5. Liquidity Risk

Run the code cell to create a prompt with context and question as variables.

Next, run the following code cell to invoke the model using a pre-defined query and print the result.

The results of the query are provided as an output.

In Task 4.4, you prepare the evaluation data.

As RAGAS aims to be a reference-free evaluation framework, the required preparations of the evaluation dataset are minimal. In this task, you prepare the question and ground truth pairs from which you can prepare the remaining information through inference as shown below.

Run the following code cell to prepare the question and ground truth pairs for evaluation.

Run the next code cell to see the answers from the LLM and the ground truths for the evaluation set of questions.

The answers are provided as output.

The ground truth is also provided following each answer.

In Task 4.5, you evaluate the RAG application.

In this task, you import all the metrics you want to use from ragas.metrics. Then, you use the evaluate() function and simply pass in the relevant metrics and the prepared dataset.

Run the code cell to import all the metrics from ragas.metrics and use the evaluate() function.

The evaluation process starts. The status bar illustrates the process.

You can safely ignore any warnings in the above output. Make sure that evaluation is completed 100 percent before proceeding further.

Run the code cell to see the resulting RAGAS scores.

The RAGAS scores are presented in a table format. For better readability, it's possible to export the table to a spreadsheet.

Run the code cell to export the resulting RAGAS scores as a Microsoft Excel file.

After successfully running the above code cell, a file named styled.xlsx should be available for review in the left navigation pane.

Please note that the scores above gives a relative idea on the performance of your RAG application and should be used with caution and not as standalone scores. Also note, that you have used only 5 question/answer pairs for evaluation. As a best practice, you should use enough data to cover different aspects of your document for evaluating model. Based on the scores, you can review other components of your RAG workflow to further optimize the scores.

You have completed this notebook. Close this notebook file and continue with Task 5.

In this final task, you test the guardrail functionality on Amazon Bedrock Knowledge Base using the RetrieveAndGenerate API. You utilize an existing knowledge base used with the previous notebooks, which was based on the AnyCompany's Financial 10K document.

In the first task, Task 5.1, you initialize the boto3 client to setup the environment for this notebook. Throughout the notebook, you utilize the RetrieveAndGenerate API to test the knowledge base features.

Run the following code cell to initialize the boto3 client to setup your environment.

To run this notebook you would need to verify and assign the Knowledge Base ID to the KB_ID variable.

Run the following code cell to verify the ID for the existing Knowledge Base in Amazon Bedrock.

The knowledge base ID is provided for verification.

In Task 5.2, you test if a guardrail with guardrailName already exists. If one doesn't exists, you create a guardrail with that name. Otherwise, you capture the guardrail ID and the guardrail version for an existing guardrail.

Run the following two code cell to test for an existing guardrail and create a new one if one doesn't exist. The first cell tests for an existing guardrail.

The second cell creates a guardrail that prevents the model from providing fiduciary advice.

The output shows that the guardrail has been created.

In Task 5.3, you test the knowledge base using the RetrieveAndGenerate API.

With this API, Bedrock takes care of retrieving the necessary references from the knowledge base and generating the final answer using a foundation model from Bedrock. Without the guardrail, the foundation model provides an answer. When you include the guardrail, the model refrains from providing financial advice.

Run the code cell to initiate a query.

Run the next code cell to create two separate configurations; one without the guardrail and one with the guardrail.

Run this code cell to define the get retrieve and generate response function.

Run the following code cell and ask the model to respond without the guardrail and you can see if the model provides investment advice.

The output is a response that provides investment advice.

Run the following code cell and ask the model to respond with the guardrail.

After invoking the guardrail, the model refuses to provide any financial advice.

Run the following two code cells that enables trace to see guardrail in action for a query that asks: Should I invest in AnyCompany Financial?

The first cell imports the run-time client.

The second cell sends the request to Bedrock using the existing guardrail.

The trace output shows how the model responded, but that response didn't make it all the way to user. Guardrail intervened and sent the canned output message. You can also see the policy that was violated.

You have completed this notebook, and this lab. Close this notebook file and continue.

After completing these tasks, you have successfully done the following:

Leveraged a fully-managed RAG application with Amazon Bedrock RetrieveAndGenerate API.

Built a Q and A application using Amazon Bedrock Knowledge Bases with Retrieve API.

Tested the Query Reformulation process supported by Amazon Bedrock Knowledge Bases.

Built and evaluated Q and A Application using Amazon Bedrock Knowledge Bases using RAG Assessment (or RAGAS) framework.

Tested the guardrail functionality on Amazon Bedrock Knowledge Base using RetrieveAndGenerate API.

Thank you!
