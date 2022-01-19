# CAP Theorem

## Concepts
- A distributed computer system can only support 2 of the 3 guarantees:
   - **Consistency**: All nodes can see the same data at the same time.
   - **Availability**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
   - **Partition tolerance**: The system continues to work despite message loss or partial failure.

     ![Screen Shot 2021-05-10 at 2 51 22 PM](https://user-images.githubusercontent.com/8989447/117723127-3b6f5300-b19f-11eb-893a-488ec6afbc46.png)

## Common Combinations
| Combination || Situations |
|----|----|
| CP (Consistency over Availability) | <li>Require atomic reads and writes. |
| AP (Availability over Consistency) | <li>Allow for eventual consistency <li>Need to continue working despite external errors. |

