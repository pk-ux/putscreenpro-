# Overview

This is a two-part trading application system that combines a Model Context Protocol (MCP) server with a Streamlit web application. The MCP server provides a standardized interface to Alpaca's Trading API, enabling LLMs to interact with stock and options trading data. The Streamlit application leverages this MCP server to create a specialized cash-secured put options analyzer that helps users find optimal income-generating opportunities while potentially acquiring stocks at a discount.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Core Components

**MCP Server Layer**: The `alpaca_mcp_server.py` serves as the primary data interface, implementing the Model Context Protocol to standardize communication between language models and Alpaca's trading services. This architectural choice allows for clean separation between data access and application logic while enabling multiple client applications to reuse the same data layer.

**Streamlit Web Application**: The `cash_secured_puts_app.py` provides an interactive web interface specifically designed for options analysis. The application imports the MCP server functions directly rather than making separate API calls, creating a tight coupling that eliminates network overhead and simplifies deployment.

## Data Processing Architecture

**Real-time Market Data Pipeline**: The system fetches live stock quotes, options data, and Greeks through Alpaca's API, with fallback mechanisms to estimated calculations when real data isn't available. This hybrid approach ensures consistent functionality even when market data has gaps.

**Parallel Processing Engine**: The Streamlit app implements concurrent processing using ThreadPoolExecutor to analyze multiple stock symbols simultaneously, significantly reducing analysis time for portfolios with many positions.

**Caching Strategy**: The system uses function-level caching (`@lru_cache`) to minimize redundant API calls during analysis sessions, improving performance and reducing API rate limit impact.

## Configuration Management

**JSON-based Configuration**: The `config.json` file centralizes default symbols, UI settings, filter parameters, and processing preferences. This approach allows users to customize the application behavior without modifying code.

**Environment-based Authentication**: API credentials are managed through environment variables and `.env` files, following security best practices by keeping sensitive information separate from the codebase.

# External Dependencies

**Alpaca Trading API**: Primary data source providing real-time and historical market data, account management, order execution, and options information. The system uses both the data API and trading API endpoints.

**Model Context Protocol (MCP)**: Framework that standardizes the interface between language models and external services, enabling seamless integration with Claude Desktop, Cursor, and VSCode.

**Scientific Computing Stack**: 
- **NumPy/SciPy**: Mathematical calculations for options pricing, probability calculations, and statistical analysis
- **Pandas**: Data manipulation and analysis, particularly for handling time series market data and options chains

**Streamlit Framework**: Web application framework providing the interactive user interface with real-time updates, progress tracking, and responsive data visualization.

**Python Environment Management**: Uses virtual environments and requirements.txt for dependency isolation and reproducible deployments across different systems.