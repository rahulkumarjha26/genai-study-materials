# Technical Interview Questions

A comprehensive collection of 117 interview questions extracted directly from handwritten technical preparation notes, categorized by domain without answers.

> 📖 **Complete Study & Revision Guide:** For plain-English, to-the-point explanations, flowcharts, and Jargon Busters for all 117 questions, see [interview_explanations.md](file:///Users/rahuljha/GENAI/interview_explanations.md).

---

## Table of Contents
1. [Gen AI & Agentic AI](#1-gen-ai--agentic-ai)
2. [Deep Learning & Computer Vision](#2-deep-learning--computer-vision)
3. [Machine Learning](#3-machine-learning)
4. [Python, Data Structures & Libraries](#4-python-data-structures--libraries)
5. [FastAPI & REST APIs](#5-fastapi--rest-apis)
6. [SQL & Database Management](#6-sql--database-management)

---

## 1. Gen AI & Agentic AI

1. Which orchestrator tool have you used?
2. Explain the RAG (Retrieval-Augmented Generation) pipeline.
3. How will you manage latency after deploying the model?
4. What are agents vs. agentic AI?
5. Suppose you're building an agentic e-commerce system like Amazon: what would be the pipeline, and which agents will you integrate?
6. How will you determine if an LLM is hallucinating or if the content retrieved is the best?
7. Where will you store embeddings for caching?
8. What are AI tools?
9. What is MCP (Model Context Protocol)?
10. What are different prompt engineering techniques?
11. What is the range and effect of the temperature parameter?
12. What are the different types of fine-tuning (e.g., Full, LoRA, QLoRA, PEFT)?
13. What types of evaluation metrics are used in RAG / Agentic AI (e.g., Ragas, faithfulness, answer relevance)?
14. Explain precision and recall in the context of RAG.
15. Which multimodal models are currently available in the market? Mention open-source options as well.
16. What are the key fine-tuning hyperparameters?
17. What is the architecture of LLaMA?
18. Which vector database have you used and why?
19. What is vector search, semantic search, cosine search, and similarity search?
20. Explain different types of vector databases.
21. What is the difference between RAG and fine-tuning? When would you choose one over the other?
22. Why do LLMs hallucinate?
23. How do you improve chunking and content retrieval?
24. Explain the architecture of a Transformer (encoder-decoder, self-attention, multi-head attention).
25. Explain the architecture of BERT and its practical uses.
26. Explain your Gen AI / Agentic AI project in detail.
27. Explain Named Entity Recognition (NER).
28. Which embedding model did you use and why?
29. Which research paper did you last read about Gen AI / Agentic AI?
30. Which is the latest RAG technique or framework you have heard of (e.g., GraphRAG, Corrective RAG, Speculative RAG)?

---

## 2. Deep Learning & Computer Vision

1. What is a perceptron?
2. How do you calculate the total number of trainable parameters in a neural network model?
3. What is an activation function?
4. What is the difference between max pooling and min pooling?
5. What is forward propagation and backward propagation?
6. If all weights and biases are initialized to zero in a CNN, will the model learn? Why or why not?
7. How does an activation function actually introduce non-linearity?
8. What is precision and recall? In cancer detection, which one is more critical and why?
9. If both precision and recall are equally important, which evaluation metric should you use?
10. Why use YOLO instead of a standard CNN for object detection? What is the structure of a YOLO model?
11. Explain the architectural structure of a Convolutional Neural Network (CNN).
12. Why prefer a CNN over an Artificial Neural Network (ANN) for image processing tasks?
13. What was the expected accuracy of your YOLO project and how did you iterate/move forward?
14. If you have to detect multiple objects in an image (e.g., baseball, cap, person, bag, table), which model architecture would you use?
15. Which models did you research or benchmark before switching to YOLO?
16. Which annotation software did you use for labeling images?
17. Explain your OCR (Optical Character Recognition) project.
18. What specific problems and challenges did you face in your OCR project?
19. Explain your YOLO project end-to-end along with its complete pipeline.
20. If you are tasked with building a face detection model to detect faces in a school, explain the step-by-step process and the libraries you would use.
21. What is a tensor?
22. What are TensorFlow, OpenCV, PyTorch, and Scikit-learn, and what are their respective roles?

---

## 3. Machine Learning

1. What is L1 (Lasso) and L2 (Ridge) regularization? How do they differ in penalty and feature selection?
2. How do decision trees work?
3. What are the key hyperparameters used in Decision Trees (e.g., max_depth, min_samples_split, criterion)?
4. Which evaluation metrics are used in Linear Regression vs. Logistic Regression?
5. What is the sigmoid function? Can softmax be used in binary Logistic Regression?
6. What is the core difference between Linear Regression and Logistic Regression?

---

## 4. Python, Data Structures & Libraries

### Core Python & OOP
1. What is the difference between multithreading, multiprocessing, and asyncio?
2. What is the difference between a set and a tuple?
3. What are class methods, instance methods, and static methods?
4. How do you make sets immutable (e.g., `frozenset`)?
5. What is a decorator and what is a generator?
6. What is Method Resolution Order (MRO) and C3 linearization?
7. What is a lambda function?
8. How does Python allocate and manage its memory (heap, reference counting, cyclic garbage collection)?
9. Explain inheritance, abstraction, encapsulation, and polymorphism in Python.
10. Explain the Global Interpreter Lock (GIL).
11. What are `*args` and `**kwargs`?
12. Which data types cannot be used as dictionary keys and why?
13. Can you rename the `self` parameter in a class method?
14. What is `__init__`? Is the `__init__` method compulsory in a class?
15. What does `if __name__ == '__main__':` do?
16. What is call by reference vs. call by value in Python (call by object reference / sharing)?
17. What is the difference between shallow copy and deep copy?
18. What is an interface, and how is it implemented in Python (e.g., using `abc.ABC` and `@abstractmethod`)?
19. What will `bool(0)` and `bool('0')` print?
20. Which is faster: a tuple or a list? Why?
21. What is the difference between call by value and call by reference?
22. Between `list.sort()` and `sorted()`, which behaves like call by value?
23. Which built-in function is built on generator principles and how does it work (e.g., `range`)?
24. If a tuple is immutable, explain why the following snippet executes without error:
    ```python
    a = [1, 2, 3]
    b = (1, 2, 3, a)
    a.append(12)
    print(b)
    # Output: (1, 2, 3, [1, 2, 3, 12])
    ```
25. What is the difference between a set and a list?
26. How are dictionaries internally stored in Python (hash table, hash collisions, compact dict layout)?
27. How are lists and tuples internally stored in memory?

### Pandas, NumPy & Data Handling
28. How do you use the `apply()` and `groupby()` functions in Pandas?
29. Explain the difference between `iloc` and `loc` in Pandas.
30. Explain `concat()` in Pandas.
31. How do you read a CSV and a text file in Python?
32. How do you rename columns in a Pandas DataFrame?
33. Why are NumPy arrays/lists faster than standard Python lists?

### Version Control & Tools
34. What are the basic Git commands (`clone`, `status`, `add`, `commit`, `push`, `pull`, `branch`, `merge`, `rebase`)?

---

## 5. FastAPI & REST APIs

1. What is dependency injection, and how does FastAPI implement it via `Depends`?
2. How do you respond fast to a user if they want to upload 100 documents simultaneously (e.g., immediate response with background tasks / asynchronous processing)?
3. How can you expose an endpoint to track how many uploads the application has processed?
4. What is the Python `requests` library?
5. What is the role of the Pydantic library in FastAPI?
6. What are standard HTTP methods (GET, POST, PUT, PATCH, DELETE, OPTIONS, HEAD)?
7. What is the difference between PUT and POST?
8. What does REST stand for, and what are the core architectural constraints of a REST API?
9. What is the difference between authentication and authorization?
10. What are the key differences between Flask and FastAPI?
11. Describe all primary API methods and their typical status codes.
12. What is Uvicorn and what is ASGI?
13. How do FastAPI and Flask process requests step-by-step internally?

---

## 6. SQL & Database Management

1. Write a SQL query to find duplicate `user_id` values based on email in an `employee` table. Also, explain potential reasons why duplicate user IDs or emails exist.
2. Write a query to find the highest salary of employees in each department.
3. Can you use `GROUP BY` with `SELECT *`? What are the limitations or dialect-specific behaviors?
4. Write an example of a subquery.
5. Write a query using a `JOIN`.
6. What is a primary key and what is a foreign key?
7. Explain the relationship and difference between foreign keys and joins.
8. Can we delete a foreign key and a primary key (constraint drops, cascading deletes, referential integrity)?
9. What is database indexing and how does it improve query performance?
10. Explain all types of SQL joins (`INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN`, `CROSS JOIN`, `SELF JOIN`).
11. What is the difference between the `WHERE` clause and the `HAVING` clause?
