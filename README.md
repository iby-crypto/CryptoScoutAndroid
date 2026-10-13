# CryptoScout Android (MVP 0.1)

A read-only Android app prototype for Binance Spot and USDⓈ-M perpetual Futures market data. It displays a candlestick chart, selected-pair live updates, a top-40 USDT quote-volume list, and a simple EMA/RSI/MACD heuristic signal.

## Important scope and safety
- **No orders are ever placed.** No API keys, login, seed phrase, wallet connection, or trading permissions are requested.
- “BUY BIAS” / “SELL BIAS” are heuristic research labels, not financial advice or validated predictions. In Spot, “SELL BIAS” means bearish/caution context and does not short a spot asset.
- Stop/target values are illustrative fixed percentages and do not account for fees, spread, slippage, funding, or liquidation.
- The initial pair list is all active USDT pairs from Binance's public exchange-info endpoint, sorted by 24h quote volume; the quick list shows the top 40. Only the selected pair's kline stream is subscribed to, to avoid opening hundreds of WebSocket streams on a phone.
- The data endpoints can be regionally restricted or rate-limited. If requests fail, check connectivity and tap Refresh.
- No guarantee of profitability. Backtest and paper-trade before using signals.

## Build an APK using Android Studio
1. Install Android Studio on a computer (Android Studio is not available as a normal APK-building app on most phones).
2. Extract this ZIP.
3. In Android Studio, choose **Open** and select the extracted `CryptoScoutAndroid` folder.
4. Allow Gradle sync. Use JDK 17 if Android Studio asks.
5. Connect an Android phone with USB debugging enabled, or create an emulator.
6. Press **Run** to install the debug build on your phone.
7. To create an APK: **Build → Build Bundle(s) / APK(s) → Build APK(s)**. Android Studio will show the output path (typically `app/build/outputs/apk/debug/app-debug.apk`).
8. Copy the APK to your phone and open it. Android may ask you to allow installation from that source; only install APKs you built or trust.

## Test checklist
- Open the app with internet access.
- Switch Spot ↔ USDⓈ-M Futures.
- Change timeframe between 1m, 5m, 15m, and 1h.
- Select BTCUSDT or another active USDT pair.
- Confirm price/candles update and indicators are populated.
- Tap Refresh after a network drop.
- Compare candles with the corresponding Binance chart. This is a prototype, not a production trading system.

## Strategy v0.1
- EMA 9 / EMA 21 trend alignment
- RSI(14) momentum band
- MACD(12,26) sign
- BUY BIAS when EMA9 > EMA21, RSI 52–68, MACD > 0
- SELL BIAS when EMA9 < EMA21, RSI 32–48, MACD < 0
- Otherwise WAIT
