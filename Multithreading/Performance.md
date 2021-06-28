## Diagrams
#### Performance metrics
![image](https://user-images.githubusercontent.com/28957748/123626185-c03f2a80-d83a-11eb-9eec-ae3754b45768.png)

![image](https://user-images.githubusercontent.com/28957748/123628739-a3f0bd00-d83d-11eb-9572-8c8f206e9d96.png)

![image](https://user-images.githubusercontent.com/28957748/123628586-786dd280-d83d-11eb-923a-3e145e028071.png)

![image](https://user-images.githubusercontent.com/28957748/123628871-c84c9980-d83d-11eb-8001-2f261ca4ed03.png)

#### Reduce latency

![image](https://user-images.githubusercontent.com/28957748/123629052-02b63680-d83e-11eb-8cea-f60efeeb8592.png)

![image](https://user-images.githubusercontent.com/28957748/123629153-25e0e600-d83e-11eb-8ad1-d247c8558cba.png)

![image](https://user-images.githubusercontent.com/28957748/123629277-4ad55900-d83e-11eb-9c5f-6f54fcd0b7d8.png)

![image](https://user-images.githubusercontent.com/28957748/123626953-99cdbf00-d83b-11eb-8345-ac658d286e41.png)

![image](https://user-images.githubusercontent.com/28957748/123627086-c8e43080-d83b-11eb-8280-b8829885670f.png)

![image](https://user-images.githubusercontent.com/28957748/123627249-f7620b80-d83b-11eb-8f25-5f2766cfebaa.png)

![image](https://user-images.githubusercontent.com/28957748/123627910-c0402a00-d83c-11eb-9c01-ba7b0de3d1a5.png)

![image](https://user-images.githubusercontent.com/28957748/123628194-04cbc580-d83d-11eb-9a1a-f70238026b5b.png)

![image](https://user-images.githubusercontent.com/28957748/123628329-29c03880-d83d-11eb-9276-7f36234f1517.png)

![image](https://user-images.githubusercontent.com/28957748/123628445-4e1c1500-d83d-11eb-87dd-4dcd0be523f9.png)

![image](https://user-images.githubusercontent.com/28957748/123628503-5ecc8b00-d83d-11eb-8e99-bfd2eff798c1.png)

![image](https://user-images.githubusercontent.com/28957748/123632924-b7525700-d842-11eb-8fcc-b2785ef0a3b8.png)

![image](https://user-images.githubusercontent.com/28957748/123632985-ce914480-d842-11eb-9f8e-b72a5f69d202.png)

#### Increase throughput 1

![image](https://user-images.githubusercontent.com/28957748/123655033-d52ab680-d858-11eb-934c-5f7296982d24.png)

![image](https://user-images.githubusercontent.com/28957748/123656442-21c2c180-d85a-11eb-8314-4d12204685da.png)

![image](https://user-images.githubusercontent.com/28957748/123656587-41f28080-d85a-11eb-9153-06585d8c0ceb.png)

#### Increase throughput 2: Schedule each task on separate thread

![image](https://user-images.githubusercontent.com/28957748/123656678-56367d80-d85a-11eb-9cea-390445680199.png)

![image](https://user-images.githubusercontent.com/28957748/123656758-68182080-d85a-11eb-963a-9f353527e6b4.png)

#### Thread pool
- Create threads once, reuse for future tasks

![image](https://user-images.githubusercontent.com/28957748/123658203-b4179500-d85b-11eb-80c7-486cee2e2cb4.png)

![image](https://user-images.githubusercontent.com/28957748/123658358-d9a49e80-d85b-11eb-9724-2813dad5277c.png)

#### Summary
![image](https://user-images.githubusercontent.com/28957748/123658533-048ef280-d85c-11eb-91f5-6fda085639d6.png)

#### Analyze
![image](https://user-images.githubusercontent.com/28957748/123664124-42dae080-d861-11eb-8368-0651ef9f707c.png)

#### Summary 2
![image](https://user-images.githubusercontent.com/28957748/123664376-7f0e4100-d861-11eb-833c-17805ea5818d.png)

## Question list
- 2 metrics to measure performance
- What is latency and throughput?
- Can we break any task into subtasks?
- How many subtasks should we break a task into? Why?
- What might be the consequences of adding more threads than number of cores?
- What are the assumptions of having n equal to number of cores in order to optimize result?
- Costs of breaking a task into many subtasks and aggregate the result?
- When does the throughput matter?
