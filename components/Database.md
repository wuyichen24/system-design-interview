# Database

## Types
### Relational and non-relational database
| | Relational database | Non-relational database |
|---|---|---|
| Alias | SQL database | NoSQL database |
| Features | <li>Rows and columns in a series of tables | <li>Schema free |
| Query Language | SQL | |
| Sub-types | | <li>Document<li>Wide-column<li>Key-value<li>Graph<li>Object<li>Tuple |

## Techniques
### Replication
| | Master-slave | Master-master |
|---|---|---|
| Architecture | ![C9ioGtn](https://user-images.githubusercontent.com/8989447/116644854-b334b680-a931-11eb-9ff5-60f57652b09d.png) | ![krAHLGg](https://user-images.githubusercontent.com/8989447/116644889-cc3d6780-a931-11eb-956d-c6eebf2f218f.png) |
| Alias | Single-leader | Multi-leader |
| Write operations | Master only  | Masters |
| Read operations | Master and slaves | Masters |

### Sharding
