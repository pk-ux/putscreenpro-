# PutScreenPro - Advanced Cash-Secured Put Options Screener

PutScreenPro is a sophisticated Streamlit web application designed to help income-focused investors find optimal cash-secured put opportunities. It combines real-time market data from Alpaca's Trading API with advanced quantitative analysis to identify the best risk-adjusted income-generating trades while potentially acquiring quality stocks at discounted prices.

## 🎯 What is Cash-Secured Put Strategy?

Cash-secured puts involve:
1. **Selling put options** on stocks you'd like to own
2. **Setting aside cash** to buy 100 shares at the strike price
3. **Collecting premium** immediately as income
4. **Two outcomes**: Either keep the premium (if stock stays above strike) or buy the stock at a discount

## ✨ Key Features

### 🔍 **Multi-Stock Analysis**
- Simultaneously screen multiple stocks for put opportunities
- Parallel processing for fast analysis of large portfolios
- Real-time market data integration through Alpaca MCP server

### 📊 **Advanced Quantitative Metrics**
- **Expected Return %**: Probability-weighted returns considering all outcomes
- **Sharpe Ratio**: Risk-adjusted performance measurement
- **Theta Efficiency**: Time decay optimization scoring
- **Volatility Risk Premium**: IV risk/reward balance analysis
- **Composite Scoring**: Multi-factor ranking system (0-100 scale)

### 🎛️ **Intelligent Filtering**
- **Risk Management**: Maximum probability of assignment (PITM)
- **Liquidity Filters**: Minimum open interest and volume requirements
- **Time Management**: Days to expiration controls
- **Custom Parameters**: Configurable through JSON or UI controls

### 📈 **Professional Analytics**
- **Real Greeks Integration**: Live Delta, Gamma, Theta, Vega from Alpaca
- **Black-Scholes Calculations**: Fallback probability modeling
- **Data Source Transparency**: Shows when using real vs. estimated data
- **Risk Assessment**: Comprehensive probability and volatility analysis

### 🎨 **User-Friendly Interface**
- **Simple Language**: "Stocks I want to own at a discount from current price"
- **Progress Tracking**: Real-time analysis progress indicators
- **Sortable Results**: Multiple sorting and filtering options
- **Educational Tooltips**: Built-in explanations of complex metrics

## 🚀 Quick Start

### Prerequisites
- Python 3.8+ 
- Alpaca Trading API account (paper or live)
- Valid Alpaca API credentials

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/putscreenpro.git
   cd putscreenpro
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up your API credentials:**
   Create a `.env` file in the project root:
   ```env
   ALPACA_API_KEY=your_alpaca_api_key
   ALPACA_SECRET_KEY=your_alpaca_secret_key
   ALPACA_PAPER_TRADE=True
   ```

4. **Run the application:**
   ```bash
   streamlit run putscreenpro.py
   ```

5. **Open your browser to:** `http://localhost:5000`

## 🔧 Configuration

### Default Settings
The application includes a `config.json` file with sensible defaults:

```json
{
  "default_symbols": "AAPL,MSFT,GOOGL,TSLA,NVDA",
  "filter_defaults": {
    "max_dte": 20,
    "max_pitm": 20,
    "min_open_interest": 10,
    "min_volume": 0
  }
}
```

### Customization
- **Stock Symbols**: Add your preferred stocks to analyze
- **Risk Parameters**: Adjust maximum assignment probability
- **Liquidity Requirements**: Set minimum open interest/volume
- **Time Horizons**: Configure days to expiration ranges

## 📊 Understanding the Metrics

### **Score (0-100)**
Proprietary composite ranking combining:
- **Expected Return** (30% weight): Probability-weighted profit projections
- **Sharpe Ratio** (25% weight): Risk-adjusted performance
- **Theta Efficiency** (25% weight): Time decay optimization
- **Volatility Risk Premium** (20% weight): IV risk/reward balance

### **Expected Return %**
More accurate than simple annualized returns:
- Considers probability of assignment using real Delta values
- Accounts for potential stock acquisition scenarios
- Provides realistic profit expectations

### **Risk Metrics**
- **PITM %**: Probability of assignment (lower = safer)
- **Sharpe Ratio**: >1.0 = excellent, 0.5-1.0 = good, <0.5 = poor
- **Distance to Strike**: Current stock price vs. strike price

### **Efficiency Metrics**
- **Theta Efficiency**: Time decay capture per dollar at risk
- **Vol Premium**: Volatility risk assessment (optimal range: 20-40% IV)

## 🏗️ Technical Architecture

### **Core Components**
- **Main Application**: `putscreenpro.py` - Streamlit web interface
- **MCP Server**: `alpaca_mcp_server.py` - Alpaca API integration layer
- **Configuration**: `config.json` - Default settings and parameters

### **Data Processing**
- **Real-time Integration**: Direct connection to Alpaca's market data
- **Parallel Processing**: Concurrent analysis using ThreadPoolExecutor
- **Caching Strategy**: Function-level caching to minimize API calls
- **Fallback Logic**: Estimated calculations when real data unavailable

### **Security**
- **Environment Variables**: API credentials stored in `.env` file
- **No Hardcoded Secrets**: All sensitive data externally configured
- **Paper Trading Default**: Safe testing environment by default

## 🎓 How to Use

### **1. Setup Your Stock List**
Enter stock symbols you'd like to potentially own at a discount:
- Format: `AAPL,TSLA,MSFT,GOOGL,NVDA`
- Focus on quality companies you'd hold long-term

### **2. Configure Risk Parameters**
- **Max DTE**: Limit to shorter expirations (typically 7-30 days)
- **Max PITM %**: Keep assignment probability low (10-25%)
- **Min OI**: Ensure liquidity (minimum 10-50 contracts)

### **3. Analyze Results**
- **Sort by Score**: Focus on highest-ranked opportunities (70+)
- **Check Risk Metrics**: Verify acceptable PITM and Sharpe ratios
- **Review Expected Returns**: Use for realistic profit projections

### **4. Risk Management**
- **Diversification**: Don't concentrate in single stocks/sectors
- **Capital Allocation**: Only use cash you'd invest in the underlying stock
- **Assignment Preparation**: Be ready to own the stock if assigned

## 📈 Strategy Guidelines

### **Conservative Approach**
- Score >60, PITM <15%, Sharpe >0.5
- Focus on blue-chip stocks with stable fundamentals
- Shorter expirations (7-21 DTE) for better control

### **Income-Focused Approach**  
- Score >50, Expected Return >10% annualized
- Balance higher premiums with acceptable assignment risk
- Consider stocks trading in reasonable valuation ranges

### **Value Acquisition Approach**
- Target stocks you want to own long-term
- Accept higher PITM for better entry prices
- Focus on high-quality companies at fair values

## 🛡️ Risk Disclaimers

**This application is for educational and analytical purposes only. It does not constitute financial advice.**

- Options trading involves substantial risk of loss
- Past performance does not guarantee future results  
- Always consult with qualified financial professionals
- Only trade with capital you can afford to lose
- Understand assignment risk and tax implications

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

## 📞 Support

For questions or support:
- Create an issue on GitHub
- Review the documentation and tooltips in the application
- Consult Alpaca's API documentation for data-related questions

---

**Happy Income Investing! 📈💰**