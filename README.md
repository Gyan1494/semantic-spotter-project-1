# Semantic Spotter Project Submission

## 1. Background

This project demonstrate "Build a RAG System" in insurance domain
using  [LangChain](https://python.langchain.com/docs/introduction/).

## 2. Problem Statement

The goal of the project is to build a robust generative search system capable of effectively and accurately
answering questions from a bunch of policy documents.

## 3. Document

1. The policy documents can be found [here](./Policy+Documents)

## 4. Approach

LangChain is a framework that simplifies the development of LLM applications LangChain offers a suite of tools,
components, and interfaces that simplify the construction of LLM-centric applications. LangChain enables developers to
build applications that can generate creative and contextually relevant content LangChain provides an LLM class designed
for interfacing with various language model providers, such as OpenAI, Cohere, and Hugging Face.

LangChain's versatility and flexibility enable seamless integration with various data sources, making it a comprehensive
solution for creating advanced language model-powered applications.

LangChain's open-source framework is available to build applications in Python or JavaScript/TypeScript. Its core design
principle is composition and modularity. By combining modules and components, one can quickly build complex LLM-based
applications. LangChain is an open-source framework that makes it easier to build powerful and personalizeable
applications with LLMs relevant to user’s interests and needs. It connects to external systems to access information
required to solve complex problems. It provides abstractions for most of the functionalities needed for building an LLM
application and also has integrations that can readily read and write data, reducing the development speed of the
application. LangChains's framework allows for building applications that are agnostic to the underlying language model.
With its ever expanding support for various LLMs, LangChain offers a unique value proposition to build applications and
iterate continuously.

LangChain framework consists of the following:

- **Components**: LangChain provides modular abstractions for the components necessary to work with language models.
  LangChain also has collections of implementations for all these abstractions. The components are designed to be easy
  to use, regardless of whether you are using the rest of the LangChain framework or not.
- **Use-Case Specific Chains**: Chains can be thought of as assembling these components in particular ways in order to
  best accomplish a particular use case. These are intended to be a higher level interface through which people can
  easily get started with a specific use case. These chains are also designed to be customizable.

The LangChain framework revolves around the following building blocks:

* Model I/O: Interface with language models (LLMs & Chat Models, Prompts, Output Parsers)
* Retrieval: Interface with application-specific data (Document loaders, Document transformers, Text embedding models,
  Vector stores, Retrievers)
* Chains: Construct sequences/chains of LLM calls
* Memory: Persist application state between runs of a chain
* Agents: Let chains choose which tools to use given high-level directives
* Callbacks: Log and stream intermediate steps of any chain

## 5. System Layers

- **Reading & Processing PDF File:** We will be using [pdfplumber](https://pypi.org/project/pdfplumber/) to read and
  process the PDF files. [pdfplumber](https://pypi.org/project/pdfplumber/) allows
  for better parsing of the PDF file as it can read various elements of the PDF apart from the plain text, such as,
  tables, images, etc. It also offers wide functionalities and visual debugging features to help with
  advanced preprocessing as well.

- **Document Chunking:** The document contains several pages and contains huge text, before generating the embeddings,
  we need to generate the chunks. Let's start with a basic chunking technique, and chunking the text with fixed size.

- **Generating Embeddings:**  Generates embedding with SentenceTransformer with all-MiniLM-L6-v2 model.

- **Store Embeddings In ChromaDB:** In this section we will store embedding in ChromaDB.

- **Semantic Search with Cache:** In this section we will introduce cache collection layer for embeddings.

- **Re-Ranking with a Cross Encoder:** Re-ranking the results obtained from the semantic search will sometime
  significantly improve the relevance of the retrieved results. This is often done by passing the query paired with each
  of the retrieved responses into a cross-encoder to score the relevance of the response w.r.t. the query.

- **Retrieval Augmented Generation:** Now we have the final top search results, we can pass it to an GPT 3.5 along
  with the user query and a well-engineered prompt, to generate a direct answer to the query along with citations.

## 6. System Architecture

![](./architecture.png)

## 7. Prerequisites

- Python 3.7+
- Please ensure that you add your OpenAI API key to the empty text file named "OpenAI_API_Key" in order to access the
  OpenAI API.

## 8. Query Screenshots

![](./queries-answer.png)