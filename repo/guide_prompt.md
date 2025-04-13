guidance prompt (to make sure it follows standards for large codebase)
指导提示（确保遵循大型代码库的标准）


---------
reference this but don’t necessarily require a formal signoff on each bullet point for every single change.

## **Guidance Prompt (for Futures Devs & AIs)**

We aim for a **7.5** on overall code quality: **professional, maintainable, and well-documented** without going overboard. Below are our core principles and structures to keep this codebase consistent and agile.

---

### **Why 7.5, Not 10?**
- **10** would mean exhaustive documentation for every class and function, near 100% test coverage, zero technical debt, hyper-detailed design artifacts, etc.
- Such a **10**-level codebase, while admirable, usually slows down agile iteration. 
- **7.5** means **clean, consistent, typed** code with well-organized services, minimal duplication, essential test coverage, and enough docs for new devs to onboard. We get the benefits of professional patterns without excessive overhead.

---

## **1. Code Organization & Layering**

1. **API Endpoints**  
   - Located under `app/api/...`  
   - Each endpoint does **request parsing**, **calls the relevant service**, and **formats the response**.  
   - Keep these routes short. Avoid any direct data transforms or business logic here.

2. **Services**  
   - Found in `lib/services/...`  
   - **Business logic** and **external integration** belong here (e.g., talking to TradeStation, Polygon).  
   - Keep them tightly focused. If services get too large, break them down or create sub-service modules.  

3. **Transformers**  
   - Located in `lib/transformers`  
   - Convert **external** data shapes to **internal** shapes (or vice versa).  
   - Refrain from inline transforms in random places—**always** go through a dedicated transformer function or module.

4. **Utilities**  
   - In `lib/utils`, subdivided (e.g., `calcUtils`, `dateUtils`, `stringUtils`).  
   - For generic calculations, parsing, or small helper logic used across modules.  
   - Keep them typed and documented.  
   - If a utility grows large or deals with a specialized domain, consider promoting it to its own specialized library or a subfolder.

5. **Context & State (Front End)**  
   - For React, we have minimal contexts like a “TradingStateContext.”  
   - Keep shapes typed and data flow straightforward—**avoid** complicated nested contexts or duplicative states.  
   - If we store positions, trades, or user data globally, ensure it’s well-labeled and typed so new devs see exactly how the data is structured.

---

## **2. Real-Time Data Strategy**

1. **Separate Real-Time Clients**  
   - Example: `PolygonStockWSClient`, `PolygonCryptoWSClient`, `TradeStationService` for streaming quotes.  
   - Each client is self-contained with **reconnection** and **subscription** logic.  
   - `RealTimeManager` (or a similar aggregator) decides which client to route calls to based on symbol or feature.  

2. **Consistent Reconnect Logic**  
   - We typically do an exponential backoff or a stable time-based reconnect.  
   - Maintain the same approach across new websockets. Don’t re-implement new patterns unless absolutely needed.

3. **Message Handling**  
   - Parse raw data, unify it into a standard shape (e.g., `Bar`, `Trade`, `Position`) via your transformers.  
   - Provide helpful error messages to the logs if something unexpected occurs.  

---

## **3. Error Handling & Logging**

1. **Centralized ErrorHandler**  
   - If possible, keep or expand a single `ErrorHandler` class (e.g. `lib/errors/ErrorHandler.ts`) to parse and log.  
   - Provide consistent error codes, e.g. `API_ERROR`, `WEBSOCKET_ERROR`, etc.  
   - For the UI or response, produce concise, user-friendly messages.

2. **Logger**  
   - Use the shared `logger.ts` with severity levels: `debug`, `info`, `warn`, `error`.  
   - Avoid scattered `console.log`. Instead, the rule of thumb is: logs that matter long-term → `logger`; ephemeral debugging logs → remove or keep behind `debug` checks.

3. **Return Structures, Not Just Strings**  
   - API endpoints typically respond with JSON: `{ error: string, details?: any }`.  
   - Avoid ambiguous messages that hamper future debugging.

---

## **4. Data Transformation Layer**

1. **Purpose**  
   - Guarantee that external data (Polygon, TradeStation, etc.) is consistently converted to our internal shapes.  
   - If the external API changes, we only update the relevant transformer.

2. **Naming Conventions**  
   - `transformTradeStationBar()`, `transformPolygonBar()`, etc.  
   - Keep function names explicit about their source (e.g. `TradeStation` or `Polygon`).

3. **Extension**  
   - If new APIs show up, add a new transformer module instead of sprinkling random conversions around.

---

## **5. Utilities Organization**

1. **Focus**  
   - `calcUtils` for numeric operations (PNL, risk, etc.).  
   - `dateUtils` for timestamps, formatting.  
   - `stringUtils` for truncation, formatting.  

2. **Documentation**  
   - A short docstring or comment block per major function helps new devs see usage quickly.  
   - Keep them typed with clear param/return signatures.

3. **Add vs. Modify**  
   - If you see a function that can be extended to handle your case, do it in one place rather than duplicating logic. 

---

## **6. Documentation**

1. **README & Folder-Level Docs**  
   - The `README.md` is our big map. If you add a new “major piece,” reference it in the README or a docs folder note.  
   - No need for enormous detail, but let folks know the existence and location of new modules.

2. **API & Services**  
   - Consider a one-liner doc block at the top of each service file describing its role.  
   - For example: “Handles integration with TradeStation’s streaming quotes, providing subscribe/unsubscribe methods.”

3. **Focus on Clarity**  
   - Our codebase’s hallmark is clarity over detail. Enough doc to let new devs jump in, not a burdensome text wall.

---

## **7. Striving for 7.5**

- We do **not** aim for “perfect” or “exhaustive.”  
- Maintain consistent patterns, typed interfaces, essential test coverage, and minimal duplication.  
- Handle known error cases gracefully.  
- This keeps the project accessible, flexible, and robust enough for real-world usage.  

### **What to do if Something Seems Lacking:**
- If a piece of the code feels duplicative or “hacked in,” refactor it into a better location or pattern—**but** keep it aligned to the existing structure.
- If you see repeated logic, unify it.  
- If a file is too big, break it out into smaller modules.  

### **What NOT to Do:**
- Don’t create elaborate abstractions or frameworks for simple tasks.  
- Don’t let style drift: keep naming, logs, doc patterns consistent.  
- Don’t bury essential logic in random places. If it’s crucial, it goes in a relevant service or utility.

---

## **8. Remember the Why**

- We want maintainable code that any new dev or AI can read, follow, and expand upon quickly.  
- We want the code to scale with new features (like new streaming providers) without big rewrites.  
- We aim to keep it clean and consistent—**that is our “7.5.”**

Following this guidance ensures the codebase remains approachable, stable, and thoroughly professional, without drowning in overengineering. Good luck and happy building!