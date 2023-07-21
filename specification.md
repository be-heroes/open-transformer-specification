# Open Transformer Specification

Version: 0.0.1

## Introduction
The Open Transformer Specification (OTS) is a specification aimed at enabling the uniform ingestion of data into Large Language Model (LLM) transformers. It is loosely derived from the [OpenTelemetry Protocol specification](https://opentelemetry.io/docs/specs/otlp/), promoting interoperability and ease of integration across various transformer implementations. OTS provides a consistent interface for data ingestion, empowering developers to seamlessly integrate LLM transformers with a wide range of applications, monitoring tools, and data analysis platforms.

## Goals
**Standardized data ingestion**: Define a common data ingestion format for LLM transformers, ensuring consistency across various implementations.

**Interoperability**: Facilitate seamless integration between LLM transformers and other systems. E.g. DLTs.

**Extensibility**: Allow for future extensions and customizations to accommodate specific use cases and evolving needs. E.g. revenue sharing.

## High-Level Architecture
OTS consists of three main components:

**Data Format Specification**: Defines the structure and contents of data that can be ingested by LLM transformers.

**API and SDK**: Provides a set of APIs and SDKs that LLM transformer implementations should follow to enable seamless integration.

**Data Collector**: An optional component that can be implemented to receive, process, and distribute data to LLM transformers. Thus enabling existing LLMs to adopt OTS simply by implementing custom exporters that target their architecture.

### Data Format Specification
The data format for OTS is based on JSON, making it easy to read, parse, and manipulate. The specification outlines the following data fields:

**timestamp**: A timestamp representing the moment when the data was generated or received.

**did**: A unique identifier for the data record.

**bid**: A unique identifier for the actor claiming ownership of the data record.

**trace_id (optional)**: A unique identifier representing a collection (or batch) of related data records, enabling distributed tracing and efficient batch processing.

**context**: A field containing contextual information related to the data record. 

**data**: The main payload, which may include the input text, tokenized text, and other relevant information.

**metadata (optional)**: Additional metadata about the data record or the transformer state.

### API and SDK
LLM transformers conforming to the OTS standard must implement the following APIs:

**ingest_data(data: JSON)**: This API is responsible for receiving data in the JSON format, as specified in the OTS standard.

**set_transformer_state(state: JSON)**: This API allows external systems to set the state of the LLM transformer (e.g., ingestion rules, filters, etc.).

**get_transformer_state() -> JSON**: This API enables external systems to query the current state of the LLM transformer.

### Data Collector (Optional)
For more complex use cases and to centralize data management, a Data Collector component can be implemented. The Data Collector is responsible for receiving data from multiple sources, process it for various purposes (anti-entropy, record revanue sharing, etc) and exporting it to one or more LLM transformers.

## Conclusion
The Open Transformer Specification (OTS) aims to streamline data ingestion for Large Language Model transformers by providing a common data format, APIs, and SDKs. OTS promotes interoperability and extensibility, providing a solid foundation for the LLM transformer ecosystem.

(Note: This is a draft specification and may require further refinement and review from the community to ensure it meets the desired objectives.)
