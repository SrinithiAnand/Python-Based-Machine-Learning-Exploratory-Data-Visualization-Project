# UK Violent Crime Analytics with Apache Spark on Azure

Scalable analysis of UK crime claims using public data and big-data tooling.  
Evaluates: (1) violent-crime trend, (2) firearms incidents per head (Liverpool vs others),  
(3) association between firearms and drug offenses.

## Data
- **Street-level crime (Home Office / Police UK)** – ~19M rows (crime type, lat/lon, month)
- **English Indices of Deprivation 2010 / LSOA population** – population + deprivation context

## Tech
PySpark 3.5 • Azure Blob Storage • Python (pandas, matplotlib, seaborn, folium) • SciPy

## Architecture / Pipeline
1. **Ingest** from Azure Blob (CSV/TXT)  
2. **Preprocess**: filter relevant crime types, handle nulls, de-duplicate (~4.49M rows removed)  
3. **Transform**: month parsing, geospatial prep, per-capita joins  
4. **Analytics**  
   - **Trend**: monthly counts, **linear regression** slope, **YoY%** with CIs  
   - **Per-capita**: incidents per 100k using LSOA population (normalize by region size)  
   - **Association**: drug vs. weapons — joint probability + spatial co-occurrence  
5. **Visualize**: time-series, bar charts (top forces), heatmaps, **Folium** incident map

## Reproducing (local or Colab)
```bash
# env
pip install pyspark pandas matplotlib seaborn folium scipy

