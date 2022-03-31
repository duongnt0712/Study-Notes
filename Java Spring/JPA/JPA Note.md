#JPA 

## 1. Architecture
Config through `persistence.xml`:
| Order 									|
| ----- 									|
| `Persistence` 								|
| `EntityManagerFactory`: create `EmtityManager` 				|
| `EntityManager`:  manage persistence operations (crud) and query entity 	|
| `Query` | `EntityManager`: manage transaction (crud)				|

## 2. GeneratedValue
- 
