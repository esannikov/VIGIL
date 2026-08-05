# World-signal sources

VIGIL uses a registry of 20 sensors. A source enters the system with an access state, temporal role, epistemic class, claim permission and known blind spots. The table below is a public summary of the registry, not runtime code.

**Registry snapshot, 5 August 2026:** 20 sources; 13 queryable in the current runtime. Access and health can change between cycles.

| Source | What it contributes | How VIGIL may use it | Current access |
|---|---|---|---|
| [USGS Earthquake Catalog](https://earthquake.usgs.gov/fdsnws/event/1/) | Time, place and magnitude of earthquakes | Exact bounded event claim; human impact requires another source | Connected |
| [GDACS](https://www.gdacs.org/) | Multi-hazard disaster alerts and modelled impact | Event context and humanitarian relevance with caveats | Intermittent |
| [WHO Disease Outbreak News](https://www.who.int/emergencies/disease-outbreak-news) | Dated outbreak reports, assessments and response | Exact claims within the report's stated scope | Connected |
| [NASA EONET](https://eonet.gsfc.nasa.gov/docs/v3) | Curated natural events such as storms, fires, volcanoes and ice events | Locate events and follow originating sources | Connected |
| [IODA](https://ioda.inetintel.cc.gatech.edu/) | Regional internet-outage alerts | Evidence of network disruption; cause remains open | Connected |
| [NOAA Space Weather](https://www.swpc.noaa.gov/) | Solar and geomagnetic alerts | Direct planetary context and temporal intensity | Connected |
| [CISA Known Exploited Vulnerabilities](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) | Vulnerabilities observed in active exploitation | Cybersecurity pressure and infrastructure exposure | Connected |
| [Federal Register](https://www.federalregister.gov/developers/documentation/api/v1) | New US federal rules, notices and policy actions | Institutional change with a clear jurisdictional boundary | Connected |
| [Wikimedia Pageviews](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) | Most-viewed pages and changes in platform attention | Attention proxy, never proof of event importance | Connected |
| [Google News RSS](https://news.google.com/rss/) | Headline discovery across publishers | Discovery only; claims return to originating reports | Limited |
| [GDELT](https://www.gdeltproject.org/) | Global news-document volume, themes and tone | Media-attention proxy and corroboration | Degraded |
| [NOAA Mauna Loa CO₂](https://gml.noaa.gov/ccgg/trends/) | Weekly atmospheric CO₂ measurement | Slow planetary substrate, not a daily event trigger by itself | Connected |
| [UNHCR Refugee Data Finder](https://www.unhcr.org/refugee-statistics/) | Displacement stocks and flows | Long-duration human context with reporting lag | Connected |
| [OpenAlex](https://docs.openalex.org/) | Scholarly works and changes in knowledge production | Research-attention and knowledge-change context | Limited |
| [World Bank Open Data](https://datahelpdesk.worldbank.org/knowledgebase/articles/889392) | Development and economic indicators | Slow baseline and structural context | Degraded |
| [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov/) | Satellite active-fire observations | Physical occurrence and spread; interpretation requires context | Access setup required |
| [ReliefWeb](https://apidoc.reliefweb.int/) | Humanitarian situation reports | Human consequence and response context | Registration required |
| [Cloudflare Radar](https://developers.cloudflare.com/radar/) | Internet outages and traffic anomalies | Regional digital disruption with stated coverage limits | Access setup required |
| [US Energy Information Administration](https://www.eia.gov/opendata/) | Energy production, supply, prices and flows | Political-economy baseline and anomaly context | Access setup required |
| [ACLED](https://acleddata.com/) | Curated political violence and protest events | Conflict-event evidence under ACLED's methodology and terms | Access setup required |

## Epistemic rule

VIGIL keeps occurrence, attention and background conditions separate. A direct record may establish that something happened. A platform metric may show where attention moved. A slow indicator may shape the day's context. None of them receives authority outside its documented scope.
