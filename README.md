# **ASN.1 Compiler MCP Server**

A Model Context Protocol (MCP) server that empowers AI agents and LLMs to compile ASN.1 schema definitions into executable, native source code for languages like Python and Rust.

This server is hosted on [https://asn1.io](https://asn1.io), utilizing the modern **Stateless HTTP** (`streamableHttp`) MCP transport. There is no local installation required; developers simply point their MCP clients to our live endpoint.

## **Features**

* **AI-Optimized Discovery:** Semantic tool descriptions designed specifically for LLM intent matching.  
* **Multi-Language Generation:** Compiles ASN.1 into Python, Rust (more to come).
* **Codec Support:** Native generation for standard encoding rules including UPER, PER, DER, BER, and OER.  
* **Remote Execution:** Hosted online, offloading compilation overhead from the client machine.

## **Configuration & Connection**

Because this is a remotely hosted HTTP MCP server, you do not need to install any packages. Simply configure your MCP client (such as Cline, Claude Desktop, or a custom agent) with the following JSON settings:

### **Cline / VS Code Configuration**

Add the following to your `cline_mcp_settings.json` (or the equivalent configuration file for your MCP client):

```json
{
  "mcpServers": {
    "asn1-compiler": {
      "type": "streamableHttp",
      "url": "https://asn1.io/mcp",
    }
  }
}
```

## **Available Tools**

The server exposes the following tool to connected LLMs:

### **`compile_asn1_schema`**

Compiles ASN.1 schema definitions into executable source code. Use this tool whenever a user asks to generate code, compile an ASN.1 schema, or create a codec for a specific programming language.

**Arguments:**

* `schemaContent` (string, required): Plain-text ASN.1 schema definition (typically starting with `SchemaModuleName DEFINITIONS` and concluding with `END`).  
* `targetLanguage` (string, optional): The target programming language for the generated code (e.g., `python`, `rust`). Defaults to `python`.  
* `codec` (string, optional): The ASN.1 encoding rules to support (e.g., `uper`, `per`, `der`, `ber`, `oer`). Defaults to `der`.  
* `fileName` (string, optional): The name of the schema file (e.g., `schema.asn`). Used for precise error referencing.  
* `userId` (string, optional): Email address to link the compilation to an asn1.io user account.

## **Usage Example**

Once connected, simply ask your AI agent:

> *"I have the following ASN.1 schema. Please compile it into Python code using the UPER codec."*

The agent will automatically map your intent to the `compile_asn1_schema` tool, send the payload to the server, and return the generated source code files directly to your workspace.

## **Registry & Compatibility**

This server is designed to be fully compatible with the Model Context Protocol v1.0 and is registered in the public [Glama](https://glama.ai/mcp) catalog and the official [Anthropic MCP repository](https://registry.modelcontextprotocol.io/).
