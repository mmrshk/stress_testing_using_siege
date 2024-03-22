# Load Testing using Siege

DB consists of 1000 Post records. Each record has 2 fields (title, body).

To create a new Post record, execute the following command:

```
1000.times do |i|
  Post.create(title: "title_#{i}", body: "body_#{i}")
end
```

In siege/ directory, there is a file called `urls.txt` which contains list of urls to run the load test.

To run load test, execute the following command:

```
brew install siege
siege -f full_path_to/siege/urls.txt -c 10 -r 2 --no-parser --no-follow
```

Results using different concurrency levels:

| Concurrency Level | Availability | Response Time | Throughput  |
|------------------| ------------ |----------|-------------|
| 10               | 100% | 0.20 secs | 0.36 MB/sec |
| 25               | 100% | 0.40 secs | 0.27 MB/sec |
| 50               | 100% | 8.09 secs     | 0.58 MB/sec |
| 100              | 100% | 16.39 secs  | 0.58 MB/sec |

