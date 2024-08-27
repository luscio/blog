---
title: GuzzleHttp并发请求
date: 2020/12/16 15:42
tags:
  - GuzzleHttp
categories:
  - GuzzleHttp
---

## 权限说明

```php
try {
    $client = new \GuzzleHttp\Client();
    // Initiate each request but do not block
    $urls = [
        'https://www.baidu.com/api/callback/authShop',
    ];
    $promises = [];
    foreach ($urls as $key => $url) {
        $options = [
            'verify' => false,
            'query' => $query,
            'form_params' => $params,
            'headers' => [],
        ];
        $promises[$key] = $client->postAsync($url, $options);
    }

    // Wait for the requests to complete, even if some of them fail
    $results = \GuzzleHttp\Promise\settle($promises)->wait();

    // You can access each result using the key provided to the unwrap
    foreach ($results as $key => $result) {
        $state = $result['state'];
        if ($state === 'rejected') {
            $exception = $result['reason'];
            $response = $exception->getResponse();
            $body = $response->getBody()->getContents();
        }
        if ($state === 'fulfilled') {
            $response = $result['value'];
            $body = $response->getBody()->getContents();
        }
    }
} catch (\Exception $exception) {
}
```