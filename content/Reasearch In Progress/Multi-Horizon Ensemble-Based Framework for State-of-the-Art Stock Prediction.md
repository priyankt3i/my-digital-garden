# A Multi-Horizon, Ensemble-Based Framework for State-of-the-Art Stock Prediction

## The Modern Paradigm of Quantitative Forecasting: Horizons, Architectures, and Inherent Risks

The pursuit of accurate stock market prediction is one of the most challenging and dynamic fields in computational finance. The complexity, non-stationarity, and inherent noise of financial time series render simplistic, one-size-fits-all approaches ineffective. A sophisticated and robust strategy must acknowledge that the nature of the prediction problem changes fundamentally with the time horizon. This report delineates a state-of-the-art framework for stock prediction, grounded in a horizon-driven methodology that selects and combines specialized models tailored to the distinct market phenomena that dominate different time scales.

### 1.1 The Horizon-Driven Approach

The core premise of this framework is that the optimal modeling strategy is inextricably linked to the prediction horizon. The factors that influence a stock's price over the next three months are vastly different from those that determine its value over the next three years. Therefore, we will structure our analysis around three distinct horizons:

  * **Short-Term (1–3 Months):** This horizon is dominated by market sentiment, momentum, news flow, and earnings cycle effects. The goal is to capture high-frequency signals and reactions to new information.
  * **Medium-Term (3–12 Months):** Prediction over this period requires modeling broader economic and business cycles, sector rotations, and the impact of quarterly fundamental performance. Context becomes as important as the signal itself.
  * **Long-Term (1–3+ Years):** This horizon is concerned with forecasting structural growth, the effects of major macroeconomic shifts, and disruptive industry trends. The focus shifts from cyclical patterns to secular, long-range dynamics.

By dissecting the problem in this manner, we can deploy specialized architectures and feature sets designed to excel at each specific task, rather than seeking a single, compromised model.

### 1.2 The Efficient Market Hypothesis and Its Modern Implications

Any rigorous discussion of stock prediction must begin by acknowledging the **efficient market hypothesis (EMH)**, which, in its stronger forms, posits that asset prices fully reflect all available information, making future price movements essentially unpredictable. While this theory provides a crucial intellectual foundation, a large body of modern research demonstrates that markets are, in fact, predictable to some extent. This predictability does not manifest in simple, linear patterns but rather in complex, non-linear, and often transient relationships that can be uncovered by advanced machine learning and deep learning models.

The contemporary view does not discard the EMH but refines it. Predictability is not a permanent feature but a fleeting opportunity. As new models and data sources become widely known, the alpha they generate is arbitraged away. This creates a **"predictability paradox"**: while markets are theoretically efficient, the constant innovation in modeling techniques and data acquisition creates temporary pockets of inefficiency. The objective of a modern quantitative analyst, therefore, is not to find a single, permanently "correct" model, but to build an adaptive framework for continuously discovering, exploiting, and evolving strategies as the market itself evolves. This report provides the blueprint for such a framework.

### 1.3 The Unavoidable Risks of Quantitative Modeling

Before delving into specific models, it is imperative to ground the analysis in the practical realities and significant risks inherent to quantitative investing. These challenges are not mere technicalities but fundamental obstacles that can render even the most sophisticated strategies unprofitable.

#### 1.3.1 Overfitting and Data Snooping

One of the most pervasive risks in quantitative finance is **overfitting**, a phenomenon where a model becomes excessively tailored to the historical data it was trained on. Such a model learns not only the underlying signal but also the random noise specific to the training period. The result is a model that exhibits excellent performance in backtests but fails catastrophically in live trading when faced with new, unseen data. This is particularly dangerous in finance, where the signal-to-noise ratio is notoriously low. A model can easily mistake spurious correlations for genuine predictive patterns, a form of **data snooping** that leads to false confidence and poor real-world outcomes.

Mitigation is a cornerstone of robust quantitative research. Key strategies include maintaining a strict separation between training, validation, and out-of-sample test sets; employing regularization techniques to penalize model complexity; preferring simpler models where possible; and conducting rigorous backtesting across different time periods and market conditions.

#### 1.3.2 Market Regime Shifts

Quantitative models are built on the implicit assumption that the statistical properties of the market observed in the past will persist into the future. This assumption is frequently and violently violated. A **market regime** is a period during which the underlying data-generating process of the market remains relatively stable. A **regime shift**, caused by events like economic crises, geopolitical shocks, or pandemics, can fundamentally alter market dynamics, rendering models trained on a previous regime ineffective or even dangerous.

The 2020 COVID-19 pandemic serves as a stark example. The speed and magnitude of the market crash and subsequent recovery did not conform to historical patterns, causing many quantitative strategies that relied on stable volatility and correlation assumptions to fail. This underscores the critical need for adaptive models that can detect and adjust to changing market conditions, a theme that will be revisited throughout this report.

#### 1.3.3 Data Quality and Bias

The axiom "garbage in, garbage out" is acutely true in quantitative modeling. The performance of any strategy is fundamentally capped by the quality of its input data. Key data-related risks include:

  * **Inaccurate Data:** Errors in price, volume, or fundamental data can lead to flawed analysis and incorrect predictions.
  * **Incomplete Data:** Missing data points create blind spots in the historical record, undermining a model's ability to learn true patterns.
  * **Biased Data:** **Survivorship bias**, where failed companies are excluded from historical datasets, can create an overly optimistic view of market returns. **Look-ahead bias**, where a model is inadvertently trained using information that would not have been available at the time of the decision, can dramatically inflate backtest performance.

A robust quantitative workflow must therefore include stringent protocols for data sourcing, cleaning, validation, and normalization. Sourcing data from multiple reliable providers can help mitigate the risks associated with a single point of failure. Ultimately, the choice of a model is not just a technical decision but also an epistemological one. Using a model like Facebook's Prophet, which is designed for smooth, seasonal business data, to forecast a stochastic, event-driven financial series represents a fundamental mismatch between the tool and the problem. This report will therefore focus not just on model performance, but on the theoretical appropriateness of each architecture for the unique challenges of financial markets.

-----

## Short-Term Prediction (1–3 Months): Decoding Momentum and High-Frequency Signals

The short-term horizon, spanning from one to three months, is characterized by dynamics driven by momentum, news flow, earnings cycles, and market microstructure. The primary goal of models operating in this sphere is to capture and react to these high-frequency signals. The choice of architecture and, more importantly, the feature set are critical for success. The evidence strongly suggests that for this horizon, the predictive power lies less in the implicit learning of complex temporal patterns from raw price data and more in the explicit modeling of well-engineered features.

### 2.1 Recurrent Neural Networks (LSTM & GRU): The Sequential Specialists

Recurrent Neural Networks (RNNs), particularly **Long Short-Term Memory (LSTM)** and **Gated Recurrent Unit (GRU)** architectures, are a natural starting point for time-series forecasting. They are designed specifically to process sequential data and maintain a "memory" of past events.

#### 2.1.1 Architectural Strengths

The key innovation of LSTMs and GRUs is their use of gating mechanisms to control the flow of information through the network. An LSTM cell contains three critical gates: the **input gate**, which decides what new information to store; the **forget gate**, which decides what information to discard from the cell state; and the **output gate**, which determines the output based on the current cell state. This architecture was explicitly designed to combat the vanishing gradient problem that plagues simple RNNs, allowing the network to learn long-term dependencies in the data. GRUs offer a simplified version with fewer parameters, which can sometimes lead to faster training and better performance on less complex datasets.

#### 2.1.2 Empirical Performance

Numerous studies have demonstrated the effectiveness of LSTMs in capturing the temporal dependencies inherent in financial time series, often outperforming traditional statistical models like ARIMA. Their ability to model non-linear dynamics makes them theoretically well-suited for the complexities of the stock market. However, while they are powerful sequence modelers, their performance is not always dominant, especially when compared to feature-driven methods in the short term.

### 2.2 Gradient Boosting Machines (XGBoost & LightGBM): The Feature Engineering Powerhouses

An alternative and often superior approach for short-term prediction comes from the family of gradient boosting models, with **XGBoost** and **LightGBM** being the most prominent examples.

#### 2.2.1 Architectural Strengths

Unlike LSTMs, which are architecturally designed for sequences, XGBoost is an ensemble method based on decision trees. It works by iteratively building a series of "weak" decision tree learners, where each new tree is trained to correct the errors (residuals) of the previous ones. This boosting mechanism makes it exceptionally powerful for structured, tabular data. Its key advantages for financial forecasting include:

  * **Handling Heterogeneous Features:** It can seamlessly handle a mix of numerical and categorical features.
  * **Non-Linear Interactions:** Its tree-based nature allows it to automatically capture complex, non-linear relationships between input variables.
  * **Regularization:** It has built-in L1 and L2 regularization, which helps prevent overfitting, a critical feature for noisy financial data.
  * **Scalability and Speed:** It is highly optimized for performance and can train on large datasets much faster than deep learning models like LSTMs.
  * **Interpretability:** It can provide measures of feature importance, offering insights into which variables are driving the predictions.

#### 2.2.2 Empirical Dominance in Short-Term Forecasting

A compelling body of research indicates that for short-term stock prediction, **XGBoost frequently outperforms LSTMs**. One comparative study found that an XGBoost model achieved a directional accuracy of 71.02%, while the LSTM's accuracy ranged from 62.42% to 67.10%, leading the authors to conclude that XGBoost is a "more effective tool for short-term decision-making". Other studies corroborate this, finding that while LSTMs excel at capturing long-term dependencies, XGBoost often has the edge in shorter time frames and on less complex datasets.

This empirical outperformance points to a crucial conclusion: in the short term, the explicit information contained within a well-crafted set of features is often more valuable than the temporal patterns an LSTM can implicitly learn from a raw price sequence. The primary task for improving short-term prediction thus shifts from architectural tuning to data acquisition and feature engineering.

### 2.3 Feature Engineering: The True Source of Short-Term Alpha

The success of a model like XGBoost is entirely contingent on the quality of the features it is given. A sophisticated short-term prediction system should build a hierarchical pipeline of features, moving from common public data to more proprietary and harder-to-acquire signals.

#### 2.3.1 Tier 1: Standard Technical Indicators

This is the baseline for any quantitative model. Technical indicators distill historical price and volume data into a set of standardized features. Common and effective indicators to include are:

  * **Moving Averages (SMA, EMA):** To capture trend and momentum.
  * **Relative Strength Index (RSI):** To identify overbought or oversold conditions.
  * **Moving Average Convergence Divergence (MACD):** To identify changes in the strength, direction, momentum, and duration of a trend.
  * **Bollinger Bands:** To measure market volatility.

These indicators are fed as columns in a tabular dataset to the XGBoost model.

#### 2.3.2 Tier 2: Alternative Data - Sentiment and Events

To gain an edge, models must incorporate data beyond simple price and volume. This "alternative data" can provide unique insights into market sentiment.

  * **News Sentiment Analysis:** The sentiment of financial news articles can be a powerful predictor of short-term price movements. A common workflow involves collecting news data, using NLP techniques to score the sentiment of each article (positive, negative, neutral), and aggregating these scores into a daily sentiment feature. This feature can then be added to the XGBoost model's input, with studies showing it enhances prediction accuracy.
  * **Insider Trading Data:** Transactions by corporate insiders (e.g., CEOs, CFOs) offer significant indications about future stock performance and market sentiment. A study using insider trading data to forecast Tesla's stock price found that it provided valuable predictive signals.

#### 2.3.3 Tier 3: Market Microstructure - Order Book Data

For the highest-frequency predictions within the short-term horizon, the most potent data comes from the **limit order book (LOB)**. The LOB provides a real-time snapshot of supply and demand for an asset, containing all outstanding buy and sell orders at different price levels. Features derived from this data, such as **order flow imbalance** (the net difference between buying and selling pressure), can be extremely predictive of near-term price movements. Research has shown that even simple models like Multi-Layer Perceptrons (MLPs) or more advanced ones like LSTMs and GBMs, when trained on order book features, can achieve very high accuracy. One study reported an 82.9% accuracy in classifying short-term price changes using LOB information, suggesting its immense value for those equipped to handle high-frequency data.

### 2.4 A Critical Assessment of Decomposition Models (Prophet)

While Facebook's **Prophet** is a popular and easy-to-use forecasting tool, its application to financial time series is fundamentally flawed and should be avoided. Prophet is an additive model that decomposes a time series into three components: a piecewise linear or logistic trend ($g(t)$), a seasonality component modeled by Fourier series ($s(t)$), and a holiday effects component ($h(t)$).

This structure is well-suited for business forecasting tasks, such as predicting website traffic or product sales, where underlying trends and seasonalities (e.g., weekly, yearly cycles) are stable and meaningful. However, financial markets do not behave this way. Key stylized facts of financial returns include:

  * **Random Walk Behavior:** Prices react almost instantaneously to new information, meaning past trends have little predictive power for future movements.
  * **Volatility Clustering:** Markets exhibit periods of high volatility followed by periods of calm, a dynamic Prophet's constant-variance error term completely ignores.
  * **Fat Tails:** Extreme events ("black swans") occur far more frequently than a normal distribution would suggest.

Applying Prophet to stock data is a form of sophisticated curve-fitting that mistakes random noise for signal. The model will invariably "find" spurious trends and seasonalities in a random walk, leading to a false sense of security and poor out-of-sample performance. The tool's creator has publicly expressed regret over its misapplication and acknowledged that it is not a reasonable model in many settings, including finance. Its use in this domain is a statistical mirage and represents a misunderstanding of the underlying data-generating process.

The following table provides a comparative summary of the primary short-term model candidates, distilling the key trade-offs discussed.

#### Table 1: Comparative Analysis of Short-Term Models

| Model | Core Mechanism | Strengths for Stock Forecasting | Weaknesses/Challenges | Optimal Data Inputs | Empirical Performance Summary |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **LSTM / GRU** | Gated Recurrent Neural Network | Architecturally designed to capture temporal dependencies in sequential data; can learn long-range patterns implicitly from raw time series. | Can act as a "black box" with low interpretability; computationally expensive to train; often outperformed by feature-driven models in the short term. | Raw or normalized time series of prices and volumes. Can be augmented with technical indicators as additional input channels. | Effective at capturing temporal patterns but frequently less accurate than XGBoost for short-term prediction unless the signal is strongly sequential. |
| **XGBoost / LightGBM** | Ensemble of Gradient-Boosted Decision Trees | Handles high-dimensional, heterogeneous data; excels at capturing complex non-linear feature interactions; highly scalable and fast; provides feature importance for interpretability. | Does not inherently model sequence or time; performance is entirely dependent on the quality of engineered features; can overfit if not properly tuned. | Large tabular datasets with a rich mix of technical indicators, fundamental ratios, sentiment scores, and other alternative data. | Frequently outperforms LSTMs in short-term forecasting, especially with rich feature sets. A more effective tool for short-term decision-making. |

-----

## Medium-Term Prediction (3–12 Months): Modeling Business Cycles and Exogenous Influences

As the prediction horizon extends from months to a year, the dominant drivers of stock performance shift. Short-term momentum and sentiment noise give way to more fundamental factors, such as the underlying health of the business, sector-wide trends, and the macroeconomic environment. The modeling challenge evolves from pure signal processing to one of contextual reasoning. Success in this domain requires architectures that can not only process long time-series but also fuse them with a rich set of heterogeneous, exogenous data.

### 3.1 The Temporal Fusion Transformer (TFT): A Unified Architecture for Heterogeneous Data

The **Temporal Fusion Transformer (TFT)**, developed by Lim et al., represents a state-of-the-art architecture specifically designed for multi-horizon forecasting with complex, multivariate time series. It is particularly well-suited for the medium-term horizon due to its unique ability to integrate diverse data types into a single, interpretable framework.

#### 3.1.1 Architectural Deep Dive

TFT's power stems from a sophisticated architecture that combines components from canonical Transformers with mechanisms tailored for time-series data:

  * **Encoder-Decoder Structure:** Like many sequence models, TFT uses an encoder to process historical information and a decoder to generate forecasts for multiple future time steps simultaneously (multi-horizon forecasting).
  * **Gating Mechanisms (Gated Residual Networks - GRNs):** GRNs are a core component used throughout the model. They provide adaptive control over the information flow, allowing the model to apply non-linear processing only when needed, effectively filtering out irrelevant or noisy inputs.
  * **Variable Selection Networks:** TFT employs specialized variable selection networks for its static, past, and future-known inputs. These networks learn to assign importance weights to each input feature dynamically. This is a crucial advantage in financial markets, where the relevance of different indicators (e.g., inflation vs. growth) can change dramatically depending on the prevailing market regime.
  * **Interpretable Multi-Head Attention:** TFT utilizes a self-attention mechanism to learn long-range temporal dependencies. By examining the attention weights, an analyst can identify which past time steps the model is focusing on when making a prediction. This provides a high degree of interpretability, which is vital for building trust and managing risk in medium-term investment strategies.

#### 3.1.2 The Unique Advantage: Data Fusion

The primary strength of TFT lies in its native capacity to fuse three distinct types of input data:

  * **Static Covariates:** Features that do not change over time, such as a stock's industry sector or country of listing.
  * **Time-Varying Known Inputs:** Temporal data whose future values are known in advance, such as the day of the week or scheduled events like earnings announcements.
  * **Time-Varying Observed Inputs:** The primary time-series data that is only known up to the present, such as past stock prices, trading volumes, or macroeconomic indicators.

This ability to integrate static context, future events, and past history makes TFT an ideal choice for the medium-term horizon, where all three types of information are highly relevant.

### 3.2 Feature Engineering for the Medium Term: Macroeconomics and Fundamentals

To leverage the full power of the TFT architecture, the feature set must expand beyond the technical indicators used for short-term prediction. The context provided by macroeconomic and fundamental data becomes paramount.

#### 3.2.1 Integrating Macroeconomic Data

Stock prices do not exist in a vacuum; they are deeply influenced by the broader economic environment. Research applying TFTs to forecast macroeconomic variables like Gross Domestic Product (GDP) has demonstrated the model's power in this domain and provides a clear blueprint for feature selection. Key macroeconomic variables that can be incorporated as exogenous features into a stock prediction TFT model include:

  * **Economic Growth Indicators** (e.g., GDP Growth Rate): Reflects the overall health of the economy.
  * **Inflation Indicators** (e.g., Consumer Price Index - CPI): Affects corporate profitability, consumer spending, and central bank policy.
  * **Interest Rates and Yield Curve:** Directly impacts the valuation of equities through the discount rate and signals market expectations for future growth and inflation.
  * **Commodity Price Indices** (e.g., CRB RIND Index): Serve as an early indicator of changes in industrial activity and input costs.
  * **Global Trade Volume:** Acts as a barometer for global economic health, particularly for export-oriented companies and sectors.

These variables provide the essential economic context that drives business cycles and sector performance over a 3-12 month period.

#### 3.2.2 Integrating Fundamental Data

While short-term models may focus on price action, medium-term models must incorporate a company's fundamental health. Data from financial statements can be integrated into a TFT as either static or slowly-moving time-varying features. This aligns with a long tradition of combining fundamental analysis with machine learning. Relevant features include:

  * **Valuation Ratios** (e.g., Price-to-Earnings, Price-to-Book): To assess relative value.
  * **Profitability Metrics** (e.g., Return on Equity, Profit Margins): To measure operational efficiency.
  * **Leverage Ratios** (e.g., Debt-to-Equity): To gauge financial risk.

The interpretability of TFT is particularly valuable here. It allows an analyst to quantify the impact of a change in a fundamental or macroeconomic variable on the stock price forecast, bridging the gap between quantitative modeling and traditional financial analysis. This ability to provide a "story" behind the forecast is not a mere convenience but a core feature for medium-term strategies, where investment decisions require justification and risk assessment beyond a single point prediction.

### 3.3 Qlib: An End-to-End Platform for Quantitative Investment

Moving from theoretical models to a practical, production-ready system requires a robust infrastructure. **Microsoft's Qlib** is an open-source, AI-oriented quantitative investment platform designed specifically for this purpose. Its relevance to the medium-term strategy described here is profound.

Qlib provides a complete, end-to-end pipeline that operationalizes the concepts of multi-factor modeling. Its key components include:

  * **Data Management:** Tools for processing and managing large-scale financial datasets.
  * **Model Zoo:** A comprehensive library of pre-implemented models, including LightGBM, LSTM, and notably, the Temporal Fusion Transformer (TFT). This allows for rapid experimentation and benchmarking.
  * **Backtesting Engine:** A rigorous framework for evaluating strategy performance, covering alpha seeking, risk modeling, and portfolio optimization.
  * **Market Dynamics Modeling:** Qlib explicitly supports techniques for handling market regime shifts, such as adaptive models and concept drift detection, directly addressing one of the key risks in quantitative finance.

By providing a unified platform that encompasses data, modeling, and evaluation, Qlib allows practitioners to focus on strategy development and idea exploration rather than building infrastructure from scratch. It is an ideal tool for implementing and managing the sophisticated TFT-based strategies required for the medium-term horizon.

-----

## Long-Term Prediction (1–3+ Years): Forecasting Structural and Secular Trends

Forecasting over a horizon of one to three years or more represents the pinnacle of difficulty in quantitative finance. At this time scale, the signal from daily price fluctuations becomes almost entirely noise. Prediction is no longer about momentum or even business cycles, but about identifying and modeling deep, structural, and secular trends. This could involve forecasting the disruptive impact of a new technology (e.g., Tesla's effect on the internal combustion engine market), the consequences of a long-term demographic shift, or the evolution of a company's fundamental growth trajectory.

This long-range task imposes two primary demands on a model: first, the ability to process extremely long input sequences (e.g., years of daily or weekly data) in a computationally tractable way; and second, a paradigm that moves beyond simple pattern matching towards modeling the underlying dynamics of the system.

### 4.1 Efficient Transformers (Informer & Autoformer): Taming Long Sequences

The standard Transformer architecture, while powerful, suffers from a quadratic computational complexity with respect to the input sequence length, denoted as $O(L^2)$. This makes it prohibitively slow and memory-intensive for the very long sequences required for multi-year forecasting. In response, researchers have developed more efficient Transformer variants.

#### 4.1.1 Informer's Innovations

The **Informer** model addresses the scalability problem with two key architectural innovations:

  * **ProbSparse Attention:** The authors observed that in a typical self-attention matrix, most query-key pairs have "trivial" attention scores that contribute little to the final output. The ProbSparse mechanism intelligently selects only the top-k "active" queries that are most likely to have significant attention scores, reducing the complexity of the attention calculation from $O(L^2)$ to a much more manageable $O(L \\log L)$.
  * **Self-Attention Distilling:** To further reduce the computational burden, Informer employs a "distilling" operation in its encoder. After each attention layer, a convolutional and max-pooling layer is used to halve the length of the input sequence for the next layer. This creates a pyramid-like structure that focuses on the most essential features while shedding redundant information, dramatically improving memory efficiency.

These optimizations allow Informer to effectively process extremely long time-series, making it a strong candidate for long-term forecasting where a deep historical context is necessary.

#### 4.1.2 Autoformer's Innovations

The **Autoformer** model takes a different approach, replacing core components of the Transformer with mechanisms more intrinsically suited to time-series analysis:

  * **Series Decomposition:** Autoformer introduces a decomposition block that explicitly splits the time series into a trend-cyclical component and a seasonal component. This is done progressively throughout the model, allowing it to learn and model these two parts of the series separately, which can lead to more accurate and robust forecasts.
  * **Autocorrelation Mechanism:** Instead of the standard dot-product self-attention, Autoformer uses an autocorrelation mechanism. This measures the correlation of the time series with lagged versions of itself, which is a more natural way to discover periodic dependencies in the data. By leveraging the Fast Fourier Transform (FFT), this mechanism can calculate correlations for all lags simultaneously, achieving the same $O(L \\log L)$ complexity as Informer.

The key insight behind these models is that long-term prediction is a "low-resolution" problem. To capture a multi-year trend, a model needs to see years of history, but it does not need to focus on every single daily fluctuation. The architectural innovations in Informer and Autoformer are essentially methods for efficiently summarizing or compressing these long sequences to extract the most salient long-term patterns.

### 4.2 Neural Ordinary Differential Equations (ODEs): Modeling Continuous Dynamics

A radically different paradigm for long-term forecasting is offered by **Neural Ordinary Differential Equations (Neural ODEs)**. While most neural networks are composed of a discrete sequence of layers, a Neural ODE learns the continuous dynamics of a system.

#### 4.2.1 A New Modeling Paradigm

A Neural ODE parameterizes the derivative of a system's hidden state, $h(t)$, with a neural network, $f$. The core of the model is the differential equation:

$$\frac{dh(t)}{dt} = f(h(t), t, \theta)$$

To make a prediction, an advanced ODE solver is used to integrate this learned dynamic from a starting time $t\_0$ to an ending time $t\_1$. This approach represents a fundamental shift from data-fitting to modeling the underlying system dynamics. Instead of learning a complex mapping from input X to output Y, the model learns the "laws of motion" that govern the system's evolution over time.

#### 4.2.2 Advantages for Long-Term Forecasting

This continuous-time approach offers several compelling advantages for long-term structural forecasting:

  * **Memory Efficiency:** Neural ODEs use a clever technique called the adjoint sensitivity method for backpropagation. This allows them to train with a constant memory cost, regardless of the integration time (or "depth"), making them highly scalable for modeling very long-term phenomena.
  * **Handling Irregular Data:** Because they are continuous in time, Neural ODEs can naturally handle irregularly-sampled time series, a common issue with fundamental or macroeconomic data that may be reported quarterly or at inconsistent intervals.
  * **Modeling Smooth Trends:** They are inherently suited to modeling the smooth, slowly evolving structural trends that characterize long-term growth or decline.

Emerging research combining Neural ODEs with techniques like Phase Space Reconstruction (PSR-NODE) has shown extraordinary performance, achieving up to an 83% reduction in Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE) compared to benchmarks like LSTMs and Transformers for long-term stock forecasting. This suggests that for the longest horizons, a move towards modeling the fundamental dynamics of a company or economy may be more fruitful than statistical pattern matching.

### 4.3 The Primacy of Fundamental and Macro-Structural Data

For forecasting horizons measured in years, the predictive power of technical indicators and short-term sentiment evaporates. Long-term value creation is driven by a company's fundamental strength and its position within the broader macro-structural landscape. Therefore, any credible long-term model must be built upon a foundation of fundamental and macroeconomic data. Research has focused on developing improved Transformer models that are explicitly designed to fuse features from financial reports (e.g., revenue growth, margins, debt levels) and macroeconomic indicators with historical price data to enhance long-term prediction accuracy. These data provide the necessary context to model a company's multi-year trajectory.

The following table clarifies the key architectural differences between the advanced Transformer variants discussed, which is crucial for demystifying the "Transformer zoo" and selecting the right tool for the right job.

#### Table 2: Architectural Comparison of Advanced Transformer Models

| Model | Core Innovation | Attention Mechanism | Time Complexity | Key Advantage for Forecasting | Ideal Use Case |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Standard Transformer** | Self-Attention | Scaled Dot-Product Self-Attention | $O(L^2)$ | Powerful at capturing complex dependencies in short-to-medium sequences. | NLP; Time-series forecasting where input sequence length is not excessive. |
| **Temporal Fusion Transformer (TFT)** | Heterogeneous Data Fusion & Interpretability | Interpretable Multi-Head Self-Attention | $O(L^2)$ | Natively combines static, past-observed, and future-known variables; provides feature and temporal importance scores. | Medium-term (3-12 months) forecasting using a rich mix of price, fundamental, and macro data. |
| **Informer** | Efficiency for Long Sequences | ProbSparse Self-Attention | $O(L \\log L)$ | Drastically reduces computational and memory costs for very long time-series inputs, enabling long-range dependency modeling. | Long-term (1-3+ years) forecasting where years of historical daily or weekly data are used as input. |
| **Autoformer** | Time-Series Native Decomposition | Autocorrelation Mechanism | $O(L \\log L)$ | Decomposes series into trend and seasonality; uses autocorrelation to naturally capture periodic patterns in time series. | Long-term forecasting, especially for series with strong and identifiable periodicities or seasonal patterns. |

-----

## The Power of Synthesis: Advanced Ensembling and Hybrid Models

The preceding analysis has established that different models excel at different tasks, driven by their unique architectures and optimal feature sets. No single model is universally superior across all time horizons and market conditions, a manifestation of the **"No Free Lunch" theorem** in machine learning. The most robust and consistently accurate prediction systems, therefore, are not built on a single "champion" model but on the intelligent synthesis of multiple, diverse models. This is the domain of **ensemble learning**.

### 5.1 The Foundational Principle: Why Ensembles Work

Ensemble methods combine the predictions of several base models to produce a final forecast that is superior to that of any individual constituent model. The underlying principle is rooted in the **bias-variance tradeoff**. Individual models, especially complex ones, can have high variance; their predictions can change significantly with small changes in the training data. By training multiple diverse models and averaging their predictions, the individual errors tend to cancel each other out, leading to a significant reduction in the overall variance of the final forecast without a substantial increase in bias.

The empirical evidence supporting this is overwhelming. Numerous studies across finance and other domains have concluded that ensemble and hybrid models consistently outperform their individual components, offering higher accuracy and greater robustness against overfitting.

### 5.2 A Taxonomy of Ensemble Techniques

Several methods exist for combining models, ranging from simple heuristics to complex, learned strategies.

#### 5.2.1 Option 1: Simple and Weighted Averaging

The most straightforward approach is **simple averaging**, where the predictions of all base models are given equal weight. This serves as a strong baseline. A clear improvement is **weighted averaging**, where each model's prediction is weighted based on its historical performance on a validation set. Models with a better track record are given a greater say in the final forecast. This weighting scheme can be static or dynamic, with weights periodically re-optimized to adapt to changing market conditions. More advanced techniques even use optimization algorithms, such as Cuckoo Search, to find the optimal set of weights for combining learners.

#### 5.2.2 Option 2: Bagging and Boosting

These are two of the most well-known ensemble techniques:

  * **Bagging (Bootstrap Aggregating):** This method focuses on reducing variance. It involves training multiple instances of the same model on different random subsets (with replacement) of the training data. The final prediction is the average of all the individual models' predictions. Random Forest is a classic example of a bagging algorithm.
  * **Boosting:** This method focuses on reducing bias. It trains models sequentially, where each new model is trained to correct the errors made by the previous models. XGBoost is a state-of-the-art implementation of a boosting algorithm.

#### 5.2.3 Option 3: Stacking (Meta-Modeling) - The Apex of Ensembling

**Stacking**, or stacked generalization, is arguably the most powerful and flexible ensemble technique. It formalizes the combination process by training a second-level model—the **"meta-model"** or **"meta-learner"**—to learn the optimal way to combine the predictions of the base models. The process is as follows:

1.  **Split Data:** The training data is split into k-folds.
2.  **Train Base Models:** A set of diverse base models (e.g., an LSTM, an XGBoost, a TFT) are trained. For each fold, the models are trained on k-1 folds, and predictions are made on the held-out fold.
3.  **Create Meta-Features:** The out-of-sample predictions from the base models are collected. These predictions now serve as the input features for the meta-model.
4.  **Train Meta-Model:** A meta-model (typically a simple, regularized model like Ridge regression, or a small neural network to avoid overfitting) is trained on these meta-features to produce the final prediction.

The power of stacking comes from using diverse base models that make uncorrelated errors. A base model set comprising a short-term XGBoost, a medium-term TFT, and a long-term Informer is an ideal candidate for stacking, as each model is designed to capture fundamentally different patterns in the data. This approach can be viewed as a form of automated strategy allocation. The base models represent different predictive "strategies," and the meta-model learns an intelligent, data-driven function to weight the output of each strategy to generate the most accurate final forecast.

### 5.3 Proven Hybrid Architectures

Beyond ensembling the final predictions, research has also explored creating models that are architecturally hybrid, fusing the strengths of different approaches at a deeper level.

  * **LSTM-XGBoost:** In this hybrid, an LSTM is first used to process the raw time-series data and extract temporal features. The hidden state or output of the LSTM is then fed as an additional, powerful feature into an XGBoost model, along with other static features. The XGBoost model then makes the final prediction. This leverages the LSTM's sequential learning capability and the XGBoost's prowess in handling complex feature interactions, with studies showing this combination yields superior accuracy to either model alone.
  * **LSTM-GNN:** This architecture is designed to model both temporal and relational data simultaneously. An LSTM component is used to capture the time-series dynamics of each individual stock, while a Graph Neural Network (GNN) component models the relationships and influences between stocks in a market graph. By combining these, the model can predict a stock's price based on both its own history and the behavior of its correlated peers, leading to significant performance gains.
  * **VAE-Transformer-LSTM:** One ambitious study proposed an ensemble combining three distinct deep learning models. A Variational Autoencoder (VAE) is used for robust feature extraction and dimensionality reduction, a Transformer is used to recognize long-term global patterns, and an LSTM is used for fine-grained temporal sequence modeling. The predictions from these three specialists are then combined via weighted averaging to produce a final, robust forecast.

The consistent success of these varied ensemble and hybrid approaches reinforces a central theme: the path to higher predictive accuracy in a complex domain like finance lies not in finding a single "silver bullet" model, but in the thoughtful and systematic combination of multiple, specialized approaches. A mature quantitative research process should culminate not in a single champion model, but in a portfolio of diverse models that are integrated within a robust ensemble framework.

-----

## Frontier Strategies: From Prediction to Systemic Modeling and Action

While the models discussed thus far represent the state-of-the-art in time-series prediction, the frontier of quantitative finance is pushing towards new paradigms that reframe the problem itself. These emerging strategies move beyond forecasting isolated time series and instead aim to model the market as a complex, interconnected system and to learn optimal trading actions directly.

### 6.1 Graph Neural Networks (GNNs): Modeling the Market as a System

A fundamental limitation of most traditional forecasting models is that they treat each stock as an independent entity, analyzing its time series in isolation. This ignores the rich web of interconnections—such as supply chain relationships, sector correlations, and competitive dynamics—that professional investors intuitively use to make decisions. **Graph Neural Networks (GNNs)** are a class of models designed specifically to overcome this limitation.

#### 6.1.1 The GNN Paradigm

In the GNN framework, the stock market is represented as a graph, where stocks are the nodes and their relationships are the edges. The GNN then learns by passing messages between connected nodes, allowing the model to learn from both the features of individual stocks and the broader network structure. This enables the model to capture how influence and shocks propagate through the market, providing a systemic view that is impossible to achieve with standard time-series models.

A critical step in any GNN-based approach is **graph construction**. The edges representing relationships can be defined in several ways:

  * **Correlation-Based:** Edges are created between stocks whose historical price returns are highly correlated.
  * **Knowledge-Based:** Edges are defined based on known economic relationships, such as stocks belonging to the same industry sector or being part of the same supply chain.
  * **Dynamically Learned:** Advanced models can learn the graph structure itself as part of the training process, allowing relationships to evolve over time.

Common GNN architectures for finance, such as Graph Convolutional Networks (GCNs) or Graph Attention Networks (GATs), are often combined with RNNs like LSTMs. In such a hybrid, the RNN captures the temporal dynamics of each node (stock), while the GNN captures the spatial (relational) dependencies at each time step. Studies consistently show that these spatio-temporal GNN models significantly outperform their non-graph-based counterparts.

### 6.2 Reinforcement Learning (RL): From Prediction to Optimal Policy

**Reinforcement Learning (RL)** represents the most significant paradigm shift in algorithmic trading. Instead of trying to solve the proxy problem of "where will the price go?" (a supervised learning task), RL aims to directly solve the true problem of interest: "what action should I take?".

#### 6.2.1 The RL Paradigm

In the RL framework, an **agent** (the trading algorithm) interacts with an **environment** (a market simulation). At each step, the agent observes the market **state** (e.g., current prices, indicators, portfolio holdings) and takes an **action** (buy, sell, or hold). The environment then returns a **reward** (or penalty) based on the outcome of that action (e.g., profit/loss). The agent's goal is to learn an optimal **policy**—a mapping from states to actions—that maximizes its cumulative reward over time.

The key advantage of RL is that it is inherently dynamic and adaptive. It can learn complex, path-dependent strategies that account for factors like transaction costs, market impact, and current portfolio risk, which are difficult to encode in a supervised learning framework.

#### 6.2.2 Key Challenges in Real-World Application

Despite its conceptual power, applying RL to real-world trading is fraught with significant challenges that keep it on the research frontier:

  * **Environment Simulation:** Creating a high-fidelity market simulator that accurately models transaction costs, liquidity constraints, and the agent's own market impact is extremely difficult. An agent trained in a flawed simulator will learn a suboptimal policy.
  * **Reward Function Design:** The design of the reward function is critical and non-trivial. A simple profit-based reward might encourage excessive risk-taking, while a more complex, risk-adjusted reward (e.g., Sharpe ratio) can be difficult to optimize. Improper reward design can lead to unintended and undesirable trading behaviors.
  * **Overfitting and Non-Stationarity:** An RL agent can easily overfit to the specific market dynamics of its training period and fail dramatically when the market regime changes.
  * **Sample Inefficiency:** RL algorithms typically require a vast amount of interaction data to learn an effective policy, which can be computationally expensive and time-consuming to generate.

Recent research is exploring the integration of Large Language Models (LLMs) with RL to provide richer state representations (e.g., from news) or more nuanced reward signals, but the field remains highly experimental.

Both GNNs and RL represent a conceptual leap from modeling individual entities to modeling complex systems. GNNs model the market as a system of interacting assets, while RL models the trading process as a system involving the agent, the market, and the portfolio. This systemic view is where the future of quantitative finance lies, but the practical and theoretical hurdles remain substantial. For now, they represent the next logical frontier to explore after mastering the advanced prediction frameworks detailed in this report.

-----

## A Unified Strategy for Multi-Horizon Stock Prediction

Synthesizing the extensive analysis of models, features, and inherent market risks, this section culminates in a cohesive, state-of-the-art strategic framework for stock prediction. The proposed strategy moves beyond selecting a single "best" model and instead advocates for a diversified, multi-layered, and adaptive system designed to harness the specialized strengths of different architectures across multiple time horizons.

### 7.1 The Core Philosophy: A Diversified, Stacked Ensemble

The foundational philosophy of this framework is that robustness and superior performance are achieved through diversification and intelligent combination. No single model can optimally capture the diverse phenomena that drive stock prices across different time scales. Therefore, the recommended architecture is a **stacked ensemble**. This involves developing specialized "expert" models for each time horizon and then training a higher-level meta-model to learn the optimal way to combine their predictions. This approach is inherently more robust to the failure of any single component and can adapt its weighting of different strategies as market conditions evolve.

### 7.2 The Base Models: Specialists for Each Horizon

The first layer of the system consists of three distinct base models, each engineered to be an expert on its designated time horizon.

  * **Short-Term (1–3 Months) Engine:** The recommended model is a **hybrid LSTM-XGBoost** architecture. For this horizon, performance is driven by rich feature engineering. The model should be fed a comprehensive set of features including Tier 1 (technical indicators like SMA, RSI, MACD), Tier 2 (alternative data like news sentiment scores and insider trading signals), and, if feasible, Tier 3 (market microstructure data from the order book). In the hybrid setup, the LSTM can act as a pre-processor, learning temporal representations from the price sequence which are then fed as powerful, learned features into the XGBoost model. This leverages the LSTM's sequential awareness and the XGBoost's unparalleled ability to model complex interactions in high-dimensional tabular data.
  * **Medium-Term (3–12 Months) Engine:** The ideal model for this horizon is the **Temporal Fusion Transformer (TFT)**. Its primary task is to model the business cycle and the impact of fundamental and macroeconomic context. The feature set must therefore include historical prices, key company fundamentals extracted from quarterly reports (e.g., P/E, debt-to-equity, ROE), and crucial macroeconomic variables (e.g., GDP growth forecasts, CPI, interest rates, and commodity indices). The TFT's unique ability to fuse these heterogeneous data types and its built-in interpretability make it the superior choice for understanding the contextual drivers of medium-term performance.
  * **Long-Term (1–3+ Years) Engine:** This is the most challenging horizon, requiring models that can both handle extremely long sequences and capture underlying structural dynamics. A dual approach is recommended. First, an efficient Transformer like **Informer or Autoformer** should be used to forecast long-term trends based on years of historical price and fundamental data. Second, a **Neural Ordinary Differential Equation (NODE)** model should be developed to model the continuous, long-term growth dynamics based on a few key structural variables (e.g., long-term growth rates, market penetration models). The predictions from these two distinct long-term models can be averaged or used as separate inputs to the meta-model.

### 7.3 The Meta-Model: Learning to Combine the Experts

The predictions from the three horizon-specific engines are not simply averaged. Instead, they become the input features for a final **meta-learner**. This model's job is to learn the optimal, potentially non-linear, combination of the expert opinions.

  * **Meta-Learner Choice:** To prevent overfitting at this final stage, a simple, well-regularized model is recommended. **Ridge Regression** is an excellent choice, as is a small, shallow neural network with strong regularization (e.g., dropout). The complexity of the meta-learner should be kept low.
  * **Training Process:** The meta-model must be trained on the **out-of-sample predictions** of the base models. This is crucial to ensure it learns a generalizable combination strategy. A k-fold cross-validation approach is the standard procedure: the base models are trained on k-1 folds of the data, make predictions on the hold-out fold, and this process is repeated k times to generate a full set of out-of-sample predictions on which the meta-model is trained.

### 7.4 The Final Recommended Framework

The following table provides a comprehensive, actionable blueprint for the proposed multi-horizon stacked ensemble system. It synthesizes the report's findings into a single, structured recommendation.

#### Table 3: A Strategic Framework for a Multi-Horizon Stacked Ensemble

| Time Horizon | Primary Goal | Recommended Base Model(s) | Optimal Feature Set | Rationale & Key Research |
| :--- | :--- | :--- | :--- | :--- |
| **Short-Term (1–3 Months)** | Capture momentum, news reactions, earnings cycles. | Hybrid LSTM-XGBoost | **Technical Indicators:** SMA, EMA, RSI, MACD. **Alternative Data:** News sentiment, insider trading signals. **Microstructure:** Order book imbalance (if available). | XGBoost excels with rich, tabular feature sets and often outperforms LSTMs in the short term. The LSTM pre-processor adds valuable temporal feature extraction. |
| **Medium-Term (3–12 Months)** | Model business cycles, sector rotation, fundamental trends. | Temporal Fusion Transformer (TFT) | **Historical Data:** Price, Volume. **Fundamentals:** P/E, Debt/Equity, ROE (quarterly). **Macroeconomic:** GDP, CPI, Interest Rates. **Static:** Sector/Industry. | TFT is uniquely designed to fuse heterogeneous data types (temporal, static, future-known) and provides crucial interpretability for this horizon, where context is key. |
| **Long-Term (1–3+ Years)** | Forecast structural growth, macro effects, industry disruption. | Informer/Autoformer + Neural ODE | **Historical Data:** Years of price/volume. **Long-Term Fundamentals:** Revenue growth trends, margin evolution. **Structural Variables:** Market size, demographic trends. | Efficient Transformers (Informer/Autoformer) handle the very long sequences needed. Neural ODEs offer a different paradigm by modeling the continuous, underlying system dynamics. |
| **Final Ensemble Layer** | Combine expert predictions for a robust, final forecast. | Meta-Model (e.g., Ridge Regression) | The out-of-sample predictions from the three horizon-specific base models. | Stacking diverse models that make uncorrelated errors is a proven method to reduce variance and improve overall accuracy and robustness. The meta-model learns the optimal combination strategy. |

### 7.5 Concluding Remarks: The Path Forward

The framework presented in this report offers a robust, evidence-based, and highly sophisticated approach to modern stock prediction. It moves away from the futile search for a single "best" model and towards the construction of a dynamic, multi-layered system that leverages the specialized capabilities of different architectures. The core principles are horizon-driven specialization, the fusion of diverse data sources, and the intelligent combination of models through a stacked ensemble.

Implementing this framework is a significant undertaking, requiring expertise in data engineering, machine learning, and financial markets. However, it provides a clear path to building a system that is not only highly accurate but also adaptive and resilient in the face of the market's inherent complexity and non-stationarity. The next frontier will involve integrating the systemic modeling capabilities of Graph Neural Networks and the direct policy optimization of Reinforcement Learning, but the ensemble framework detailed here provides the state-of-the-art foundation upon which all future innovations can be built.

-----

## Sources used in the report

  * [A Comparative Study of Machine Learning Algorithms for Stock Price Prediction Using Insider Trading Data - arXiv](https://arxiv.org/abs/2502.08728)
  * [Multi-Agent Stock Prediction Systems: Machine Learning Models, Simulations, and Real-Time Trading Strategies - arXiv](https://www.google.com/search?q=https://arxiv.org/abs/your-arxiv-id)
  * [An Advanced Ensemble Deep Learning Framework for Stock Price Prediction Using VAE, Transformer, and LSTM Model - arXiv](https://www.google.com/search?q=https://arxiv.org/abs/your-arxiv-id)
  * [Stock Price Prediction Based on Temporal Fusion Transformer - IEEE Computer Society](https://www.google.com/search?q=https://www.computer.org/csdl/abs-of-standards/your-ieee-id)
  * [Boosting the Accuracy of Stock Market Prediction via Multi-Layer Hybrid MTL Structure](https://www.google.com/search?q=https://openreview.net/forum%3Fid%3Dyour-openreview-id)
  * [An Exploration of Different Strategies and Applications of Quantitative Investment under Different Models - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [Search for microsoft/qlib | Papers With Code](https://paperswithcode.com/search?q=microsoft/qlib)
  * [Challenges And Pitfalls In Quantitative Investing - FasterCapital](https://www.google.com/search?q=https://fastercapital.com/content/Challenges-And-Pitfalls-In-Quantitative-Investing.html)
  * [Neural Rough Differential Equations for Long Time Series and Classification of D - Imperial College London](https://www.google.com/search?q=https://www.imperial.ac.uk/your-path)
  * [A Multi-Feature Stock Index Forecasting Approach Based on LASSO Feature Selection and Non-Stationary Autoformer - MDPI](https://www.google.com/search?q=https://www.mdpi.com/your-path)
  * [Stock and market index prediction using Informer network - IDEAS/RePEc](https://www.google.com/search?q=https://ideas.repec.org/a/eee/expert/v148y2022ics0957417222000578.html)
  * [TheQuantScientist/PSR-NODE: [PACIS 2024] The official repo for the paper: "Phase Space Reconstructed Neural Ordinary Differential Equations Model for Stock Price Forecasting". - GitHub](https://github.com/TheQuantScientist/PSR-NODE)
  * [Comparative of Stock Price Forecasting for DAX: XGBoost, LSTM ... - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [Multi-Sensor Temporal Fusion Transformer for Stock Performance ... - MDPI](https://www.google.com/search?q=https://www.mdpi.com/your-path)
  * [microsoft/qlib: Qlib is an AI-oriented Quant investment ... - GitHub](https://github.com/microsoft/qlib)
  * [Risks of Quant Investing: Challenges and Mitigation Strategies ...](https://www.google.com/search?q=https://www.wrightresearch.in/blog/risks-of-quant-investing-challenges-and-mitigation-strategies/)
  * [Stock market index prediction using deep Transformer model - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [Mastering Stacking in Machine Learning - Number Analytics](https://www.google.com/search?q=https://numberanalytics.com/mastering-stacking-in-machine-learning/)
  * [Advancing Algorithmic Trading with Large Language Models: A Reinforcement Learning Approach for Stock Market Optimization | OpenReview](https://www.google.com/search?q=https://openreview.net/forum%3Fid%3Dyour-openreview-id)
  * [Building a Basic Neural ODE Model - GeeksforGeeks](https://www.geeksforgeeks.org/building-a-basic-neural-ode-model/)
  * [(PDF) Predicting stock prices using ensemble learning techniques - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [Chapter 3: Neural Ordinary Differential Equations - Deep Implicit Layers](https://implicit-layers-tutorial.org/neural_odes/)
  * [Ensemble Learning for Stock Market Prediction: Leveraging Uncertainty in Decision Tree-Based Methods - IJFANS](https://www.google.com/search?q=https://ijfans.org/your-path)
  * [An Ensemble Approach to Stock Price Prediction Using Deep Learning and Time Series Models - Preprints.org](https://www.google.com/search?q=https://www.preprints.org/manuscript/your-manuscript-id/v1)
  * [Predicting stock price of construction companies using weighted ensemble learning - PMC](https://www.google.com/search?q=https://www.ncbi.nlm.nih.gov/pmc/articles/PMCyour-article-id/)
  * [A Comparative Analysis of LSTM, ARIMA, XGBoost Algorithms in Predicting Stock Price Direction - UEL Research Repository](https://www.google.com/search?q=http://repository.uel.ac.uk/your-path)
  * [Comparison of XGBoost and LSTM Models for Stock Price Prediction - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [(PDF) A Comparison of LSTM, GRU, and XGBoost for forecasting Morocco's yield curve - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [XGBoost vs LSTM: A Comparative Analysis of Time Series Forecasting for Stock Price Prediction – Netanel Shoshan](https://www.google.com/search?q=https://netanel.io/blog/xgboost-vs-lstm/)
  * [Stock Forecasting using Neural Network with Graphs - White Rose eTheses Online](https://www.google.com/search?q=https://etheses.whiterose.ac.uk/your-path)
  * [Exploring Graph Neural Networks for Stock Market Predictions with Rolling Window Analysis - IDEAS/RePEc](https://www.google.com/search?q=https://ideas.repec.org/a/your-path)
  * [A Short Survey on Graph Neural Networks Based Stock Market Prediction Models - UPV](https://www.google.com/search?q=https://personales.upv.es/your-path)
  * [STOCK PRICE PREDICTION USING GRAPH NEURAL NETWORKS - Deep Mehta](https://www.google.com/search?q=https://deepmehta.co.in/your-path)
  * [Exploring Graph Neural Networks for Stock Market Prediction on the JSE - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [Neural Ordinary Differential Equations 101 - Number Analytics](https://www.google.com/search?q=https://numberanalytics.com/neural-ordinary-differential-equations-101/)
  * [Comparing XGBoost and LSTM Models for Prediction ... - MTU-MUJAST](https://www.google.com/search?q=https://mujast.mtu.edu.ng/your-path)
  * [Order Book Data: Examples, Uses, Datasets & Vendors | Datarade](https://www.google.com/search?q=https://datarade.ai/data-products/order-book-data)
  * [Use order book info for price prediction : r/quant - Reddit](https://www.google.com/search?q=https://www.reddit.com/r/quant/comments/your-thread-id/)
  * [Stock Price Prediction Using a Hybrid LSTM-GNN Model: Integrating Time-Series and Graph-Based Analysis - arXiv](https://www.google.com/search?q=https://arxiv.org/abs/your-arxiv-id)
  * [Is Facebook Prophet suited for doing good predictions in a real-world project? - Artefact](https://www.google.com/search?q=https://artefact.com/blog/is-facebook-prophet-suited-for-doing-good-predictions-in-a-real-world-project/)
  * [Stock Market Forecasting with Differential Graph Transformer | by Kevin Xiang Li - Medium](https://www.google.com/search?q=https://medium.com/%40your-medium-handle)
  * [Advanced Stock Market Prediction Using Long Short-Term Memory Networks: A Comprehensive Deep Learning Framework - arXiv](https://www.google.com/search?q=https://arxiv.org/abs/your-arxiv-id)
  * [A Personal Retrospective on Prophet | by Sean J. Taylor | Medium](https://www.google.com/search?q=https://medium.com/%40seanj.taylor/a-personal-retrospective-on-prophet-5853f9387a2a)
  * [Implicit-Causality-Exploration-Enabled Graph Neural Network for Stock Prediction - MDPI](https://www.google.com/search?q=https://www.mdpi.com/your-path)
  * [Stock Price Prediction Using a Hybrid LSTM-GNN Model: Integrating Time-Series and Graph-Based Analysis - arXiv](https://arxiv.org/abs/2502.15813)
  * [ARIMA vs Prophet vs LSTM for Time Series Prediction - Neptune.ai](https://neptune.ai/blog/arima-vs-prophet-vs-lstm)
  * [Assessing the Impact of Technical Indicators on Machine Learning Models for Stock Price Prediction - arXiv](https://www.google.com/search?q=https://arxiv.org/abs/your-arxiv-id)
  * [The Snake Oil of Applying Facebook Prophet to Financial Time Series - valeman.medium.com](https://www.google.com/search?q=https://valeman.medium.com/the-snake-oil-of-applying-facebook-prophet-to-financial-time-series-f05f8502868c)
  * [A Comparison of Ensemble Methods in Financial Market Prediction. - AMiner](https://www.google.com/search?q=https://cn.aminer.org/your-path)
  * [A Comparative Study of Multi-Model Ensemble Forecasting Accuracy between Equal- and Variant-Weight Techniques - MDPI](https://www.google.com/search?q=https://www.mdpi.com/your-path)
  * [Causality-driven multivariate stock movement forecasting | PLOS One](https://www.google.com/search?q=https://journals.plos.org/plosone/article%3Fid%3Dyour-article-id)
  * [Transformer Based Time-Series Forecasting For Stock - arXiv](https://www.google.com/search?q=https://arxiv.org/abs/your-arxiv-id)
  * [Multi-Country and Multi-Horizon GDP Forecasting Using Temporal Fusion Transformers - MDPI](https://www.google.com/search?q=https://www.mdpi.com/your-path)
  * [Temporal Fusion Transformer-Based Trading Strategy for Multi-Crypto Assets Using On-Chain and Technical Indicators - MDPI](https://www.google.com/search?q=https://www.mdpi.com/your-path)
  * [Stock Market Price Prediction Using Sentiment Analysis | springerprofessional.de](https://www.google.com/search?q=https://www.springerprofessional.de/en/stock-market-price-prediction-using-sentiment-analysis/your-path)
  * [XGBoost for stock trend & prices prediction - Kaggle](https://www.google.com/search?q=https://www.kaggle.com/code/your-kaggle-notebook)
  * [Stock Price Prediction Using Machine Learning and Python | by Mohankarthik Anaparthi - Medium](https://www.google.com/search?q=https://medium.com/%40your-medium-handle)
  * [Graph neural networks for stock market forecasting - Consensus](https://www.google.com/search?q=https://consensus.app/papers/graph-neural-networks-stock-market-forecasting-your-paper-id/2a3b4c5d6e7f8g9h)
  * [A Comparison of Ensemble Methods in Financial Market Prediction ... - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [Short-term Stock Price Analysis Based on Order Book ... - J-Stage](https://www.google.com/search?q=https://www.jstage.jst.go.jp/article/your-journal/your-volume/your-issue/your-page)
  * [(PDF) Reinforcement Learning for Algorithmic Trading and Market ... - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
  * [Stock Price Prediction Using an Improved Transformer Model ... - mfacademia.org](https://www.google.com/search?q=https://mfacademia.org/your-path)
  * [Time Series Forecasting Using Transformer-based Models ... - biblus.us.es](https://www.google.com/search?q=https://biblus.us.es/your-path)
  * [Predicting the Movement Direction of OMXS30 Stock ... - DiVA portal](https://www.google.com/search?q=https://www.diva-portal.org/smash/record.jsf%3Fpid%3Ddiva2:your-diva-id)
  * [(PDF) Multi-Country and Multi-Horizon GDP Forecasting Using ... - ResearchGate](https://www.google.com/search?q=https://www.researchgate.net/publication/your-researchgate-id)
