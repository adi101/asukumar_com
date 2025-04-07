# Will applications become infrastructure?

Based on some very rough napkin math, the market cap of top public tech companies is split 50-50 between infrastructure-layer companies (like Nvidia, Oracle, AWS, Azure, etc.) and application-layer companies (like Apple, Google, Facebook, Microsoft ex. Azure, etc.).[^1]

Private market valuations (putting aside OpenAI and Anthropic) are skewed towards applications - about 60-40.[^2]

There are two views of where we go from here.

The first is that the foundational models become a pseudo infrastructure layer, with apps continuing to own the interface between the customer and the product:

user <-ui-> app <-api-> model <-storage/compute-> infra

In this world, applications continue to enjoy the advantages they have today. They can build moats through their customer relationships[^3], they have pricing power because of those moats, and they have operating leverage with very low variable costs. And as inference continues to get cheaper, those variable costs do as well.

But there's another view of the world: one where the model is what the customer is interacting with, and the app is just a service that the model can access (through an [mcp server](https://modelcontextprotocol.io/introduction)):

user <-agent-> model <-mcp-> app <-storage/compute-> infra

It's hard to see tranditional enterprise software capturing the same amount of value in this world. There's no switching cost!

Take CRMs. A sales rep doesn't care whether their AI model is pulling customer data from Hubspot or Salesforce. Sure - the data might be stored in a different way in one vs. the other[^4]. But it'll get presented to the user in the same interface by ChatGPT, or Claude, or Gemini, or whatever.

To that point - what if the data's just stored in a Postgres databse somewhere? If the model knows where the information you need is, when you need it, why can't it just talk to the database[^5] and pull the data directly?

Of course, apps aren't just a CRUD UI on top of a database. They have role-based access control and use domain-specific logic - both of which make them critical for enterprises. The real question is whether those functions can be brought into the model layer.

Can you imagine a world where, based on raw customer data stored in a database, an agent client could generate a sales email? Or a financial forecast? What if the agent was the one determining which database records you have access to, based on what it knows about your role?[^6]

Not everything would be done through a text/chat interface. What if, when necessary, the agent generated a custom UI for a discrete human interaction?[^7]

If you believe in this second view of the world, there's about 50% of public (and 60% of private) tech company value that's waiting to be eaten by foundational models and their client agents. In this world, applications are just databases and servers. In other words, infrastructure.

---

[^1]: I looked at the top ~25 public tech companies globally by market cap and organized them into "application" or "infrastructure" - for companies like Amazon where it was a mix, I estimated the share of market cap that each "side" represented

[^2]: For privates, I did the same, but with the [Forbes Cloud 100](https://www.forbes.com/lists/cloud100/)

[^3]: "Customer relationships" is doing a lot of heavy lifting here. Let's call this a proxy for network effects, switching costs, differentiated distribution, and whatever else makes an app stick

[^4]: These two CRMs are different in many many ways, a lot of which can be abstracted to "they store data differently" on the backend, but some of which cannot (e.g., they have fundamentally different options of what "companies" "contacts" or "leads" are). And of course they have fundamentally different ways of enabling sellers/marketers to build workflows and automations. The idea is that this stuff could be pulled into the agent layer.

[^5]: In this case the MCP server would not be touching an app but rather a data warehouse/lakehouse. Like [this MCP server](https://github.com/morningman/mcp-doris) for Apache Doris. Please don't actually try to use this as your CRM.

[^6]: Role-based access control is the critical thing that needs to be solved for this to work for enterprises. How do you prevent agents from only accessing, modifying, or deleting records that they should be able to?

[^7]: Karri Saarinen from Linear has [a great post](https://linear.app/blog/design-for-the-ai-age) that takes the other side of this bet