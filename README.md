# GovBR News Agencies Database

Complete database of Brazilian government agencies with news feeds.

## Overview

This repository contains structured data about 156 Brazilian government agencies, including their official names, institutional classifications, hierarchical relationships, and news feed URLs.

## Files

### `agencies.yaml`

Complete database with all agency information:

- **name**: Official name in Portuguese
- **type**: Institutional classification (Ministério, Agência, Instituto, Fundação, etc.)
- **parent**: Parent organization key (see hierarchy.yaml)
- **url**: News feed URL

**Example:**
```yaml
sources:
  mcti:
    name: "Ministério da Ciência, Tecnologia e Inovação"
    type: "Ministério"
    parent: "presidencia"
    url: "https://www.gov.br/mcti/pt-br/acompanhe-o-mcti/noticias/ultimas-noticias"
```

### `hierarchy.yaml`

Visual tree structure showing organizational relationships using acronyms only.

**Example:**
```yaml
presidencia:
  - mcti:
      - inpe
      - inpa
      - cnen:
          - cdtn
          - ien
```

## Statistics

- **Total agencies**: 156
- **Institutional types**: 29 different classifications
- **Hierarchy levels**: 4 (Presidência → Ministries → Agencies → Sub-units)
- **Coverage**: All federal government agencies with public news feeds

## Top Parent Organizations

| Parent | Children | Full Name |
|--------|----------|-----------|
| mcti | 21 | Ministério da Ciência, Tecnologia e Inovação |
| gestao | 12 | Ministério da Gestão e da Inovação em Serviços Públicos |
| cultura | 8 | Ministério da Cultura |
| saude | 7 | Ministério da Saúde |
| fazenda | 7 | Ministério da Fazenda |

## Institutional Types

The database includes 29 different types of government entities:

- Ministério (29)
- Instituto (24)
- Agência (14)
- Autarquia (14)
- Centro (12)
- Secretaria (11)
- Fundação (9)
- Portal (6)
- And 21 more specialized types

## Usage

### Python

```python
import yaml

with open('agencies.yaml', 'r', encoding='utf-8') as f:
    data = yaml.safe_load(f)
    agencies = data['sources']

# Get all ministries
ministries = {k: v for k, v in agencies.items() if v['type'] == 'Ministério'}

# Get children of a specific parent
mcti_children = {k: v for k, v in agencies.items() if v['parent'] == 'mcti'}
```

### JavaScript/Node.js

```javascript
const yaml = require('js-yaml');
const fs = require('fs');

const data = yaml.load(fs.readFileSync('agencies.yaml', 'utf8'));
const agencies = data.sources;

// Get all agencies with news URLs
const newsFeeds = Object.entries(agencies).map(([key, agency]) => ({
  key,
  name: agency.name,
  url: agency.url
}));
```

## Data Quality

✅ **Complete**: All 156 agencies have complete metadata
✅ **Validated**: All parent references are valid
✅ **Consistent**: Uniform structure across all entries
✅ **Up-to-date**: Last updated October 2025

## Research Methodology

The data was compiled through:

1. Official gov.br website analysis
2. Legal documentation and founding laws
3. Institutional structure research (vinculação)
4. Manual verification of news feed URLs

## Contributing

To suggest corrections or additions:

1. Verify information from official government sources
2. Ensure URLs point to valid news feeds
3. Maintain YAML structure consistency
4. Submit pull request with detailed explanation

## License

This data is compiled from public government sources and is provided for informational purposes.

## Maintained By

[Destaques Gov.br](https://github.com/destaquesgovbr)

---

**Last Updated**: October 25, 2025
**Version**: 1.0.0
