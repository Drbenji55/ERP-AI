# ERP-AI — AI-Powered ERP Automation with n8n

An educational ERP automation project that connects **n8n**, **AI agents**, **Airtable**, and **Telegram**. The current repository includes a manager-facing agent that can answer operational questions, search business records, and create tasks through natural-language conversation.

> **Portfolio note:** This is a learning-project implementation by the repository owner. It is based on the AI-ERP course project and architecture published by [Tomer Fooks](https://github.com/tomerfooks/ai-erp-n8n). See [Attribution](#attribution) for details.

**[עברית](#erp-ai--אוטומציית-erp-מבוססת-ai-עם-n8n)**

## What is included

| Component | Purpose | Status |
|---|---|---|
| `6 - Manager Agent.json` | Importable n8n workflow for a Telegram-based manager agent | Included |
| Telegram access check | Restricts the manager bot to the configured owner chat ID | Included |
| AI manager | Answers in the user's language and uses connected tools | Included |
| Airtable tools | Searches invoices and tasks and creates new tasks | Requires configuration |
| Policy retrieval | Exposes an in-memory vector store to the agent as a retrieval tool | Requires indexed content |
| Conversation memory | Keeps a short per-chat context window | Included |

## Architecture

```text
Manager on Telegram
        │
        ▼
 Telegram Trigger ──▶ Owner Check ──▶ AI Manager Agent ──▶ Telegram Reply
                                           │
                       ┌───────────────────┼───────────────────┐
                       ▼                   ▼                   ▼
                Airtable Search     Create a Task       Policy Retrieval
              invoices and tasks                         (vector store)
```

The agent is designed to use tools instead of relying only on model memory. That makes it suitable for questions about revenue, outstanding invoices, open tasks, and internal policies, while also allowing the manager to create a task from Telegram.

## Technology

`n8n` · `AI agent and tool calling` · `OpenAI-compatible chat model` · `RAG / vector store` · `Airtable` · `Telegram Bot API`

## Getting started

1. Download `6 - Manager Agent.json` from this repository.
2. In n8n, choose **Import from File** and select the workflow JSON.
3. Create your own Telegram bot and connect its credential in n8n.
4. Connect your own Airtable and AI-provider credentials.
5. Configure `OWNER_TELEGRAM_CHAT_ID` and `AIRTABLE_BASE_ID` in your n8n environment.
6. Select the correct Airtable tables and map their fields in the three Airtable tools.
7. Load your policy content into the vector store or replace it with a persistent vector database.
8. Test every tool, then activate the workflow.

Never publish API keys, access tokens, personal customer data, or production credentials. Credential references contained in an exported workflow must be remapped to credentials owned by the person deploying it.

## Current limitations

- The repository currently exposes the manager-agent workflow; the complete multi-workflow ERP suite is not included here.
- Airtable table selection and field mapping must be adapted to the target base.
- The included conversation memory and vector store are in-memory and are not intended for durable production storage.
- The workflow is imported inactive and should be tested with non-production data before activation.
- This is a portfolio and training project, not a production-ready ERP product.

## Attribution

This implementation was created as part of a learning project based on the concepts, requirements, and reference architecture taught and published by **Tomer Fooks** in [tomerfooks/ai-erp-n8n](https://github.com/tomerfooks/ai-erp-n8n). The README in this repository is original and describes the files that are actually present here.

---

# ERP-AI — אוטומציית ERP מבוססת AI עם n8n

פרויקט לימודי לאוטומציית ERP המחבר בין **n8n**, **סוכני AI**, **Airtable** ו-**Telegram**. המאגר כולל כרגע סוכן מנהל שמקבל שאלות בשפה טבעית, מחפש מידע עסקי ויוצר משימות מתוך שיחת טלגרם.

> **הערה לתיק העבודות:** זו מימוש לימודי של בעל המאגר, המבוסס על פרויקט ה-AI-ERP והארכיטקטורה שפרסם [Tomer Fooks](https://github.com/tomerfooks/ai-erp-n8n). פרטים נוספים נמצאים בסעיף [קרדיט ומקור](#קרדיט-ומקור).

**[English](#erp-ai--ai-powered-erp-automation-with-n8n)**

## מה כלול במאגר

| רכיב | תפקיד | מצב |
|---|---|---|
| `6 - Manager Agent.json` | workflow לייבוא ל-n8n עבור סוכן מנהל בטלגרם | כלול |
| בדיקת הרשאת טלגרם | מגבילה את הבוט למזהה הצ'אט של הבעלים | כלול |
| סוכן מנהל | משיב בשפת המשתמש ומפעיל כלים מחוברים | כלול |
| כלי Airtable | חיפוש חשבוניות ומשימות ויצירת משימה | דורש הגדרה |
| שליפת נהלים | vector store בזיכרון שנחשף לסוכן ככלי RAG | דורש טעינת תוכן |
| זיכרון שיחה | שומר חלון הקשר קצר ונפרד לכל צ'אט | כלול |

## ארכיטקטורה

```text
מנהל בטלגרם
      │
      ▼
Telegram Trigger ──▶ בדיקת בעלים ──▶ סוכן מנהל ──▶ תשובה בטלגרם
                                          │
                      ┌───────────────────┼───────────────────┐
                      ▼                   ▼                   ▼
             חיפוש ב-Airtable       יצירת משימה        שליפת נהלים
             חשבוניות ומשימות                          (Vector Store)
```

הסוכן מתוכנן להפעיל כלים ולקבל מהם נתונים, ולא להסתמך רק על הידע של המודל. כך ניתן לשאול על הכנסות, חשבוניות פתוחות, משימות ונהלים פנימיים, וגם ליצור משימה חדשה ישירות מטלגרם.

## טכנולוגיות

`n8n` · `סוכן AI ו-Tool Calling` · `מודל שיחה תואם OpenAI` · `RAG / Vector Store` · `Airtable` · `Telegram Bot API`

## הפעלה ראשונית

1. מורידים מהמאגר את `6 - Manager Agent.json`.
2. ב-n8n בוחרים **Import from File** ומייבאים את הקובץ.
3. יוצרים בוט טלגרם אישי ומחברים את ה-credential שלו ב-n8n.
4. מחברים credentials אישיים של Airtable ושל ספק ה-AI.
5. מגדירים בסביבת n8n את `OWNER_TELEGRAM_CHAT_ID` ואת `AIRTABLE_BASE_ID`.
6. בוחרים את טבלאות Airtable המתאימות וממפים את השדות בשלושת כלי Airtable.
7. טוענים את מסמכי הנהלים ל-vector store, או מחליפים אותו במסד וקטורי קבוע.
8. בודקים כל כלי בנפרד ורק לאחר מכן מפעילים את ה-workflow.

אין לפרסם מפתחות API, אסימוני גישה, נתוני לקוחות או credentials של סביבת ייצור. לאחר הייבוא יש למפות מחדש את כל הפניות ל-credentials לחשבונות של מי שמפעיל את המערכת.

## מגבלות נוכחיות

- המאגר כולל כרגע את workflow סוכן המנהל; חבילת ה-ERP המלאה ורבת ה-workflows אינה נמצאת כאן.
- יש להתאים את בחירת טבלאות Airtable ומיפוי השדות לבסיס הנתונים של ההתקנה.
- זיכרון השיחה וה-vector store שב-workflow נשמרים בזיכרון ואינם אחסון קבוע לסביבת ייצור.
- ה-workflow מיובא במצב לא פעיל ויש לבדוק אותו מול נתוני ניסוי לפני הפעלה.
- זהו פרויקט לימודי ותיק עבודות, ולא מוצר ERP מוכן לסביבת ייצור.

## קרדיט ומקור

המימוש נוצר כחלק מפרויקט לימודי המבוסס על הרעיונות, הדרישות וארכיטקטורת הייחוס של **Tomer Fooks**, כפי שפורסמו במאגר [tomerfooks/ai-erp-n8n](https://github.com/tomerfooks/ai-erp-n8n). ה-README במאגר זה נכתב מחדש ומתאר את הקבצים שנמצאים בו בפועל.
