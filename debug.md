# debug

```shell

npm install
# 输出报文到文件
export ENABLE_REQUEST_LOGS=true
# 运行起来
npm run dev

   -  会在 标准输出 看到关键 EFFORT 日志 
         [01:59:26] [Effort] Claude→OpenAI: "high"
         [12:34:56] [Effort] To https://api.anthropic.com/v1/messages (claude-3-7-sonnet-20250219): "high"
                  
   - ENABLE_REQUEST_LOGS
      当前运行目录下的 报文 日志 ，  想看 effort 转换的话，关注 1 → 3 或 4 就够了
         logs/{sourceFormat}_{targetFormat}_{model}_{timestamp}/
                     ├── 1_req_client.json    ← 客户端原始请求
                     ├── 2_req_source.json   ← 标准化后的源格式
                     ├── 3_req_openai.json   ← 转换为 OpenAI 中间格式
                     ├── 4_req_target.json   ← 最终发送给上游的请求  ，  可以看这个文件 ！！！！ body 中的 reasoning_effort
                     ├── 5_res_provider.txt    上游返回的原始响应（流式）  
                     ├── 7_res_client.txt      返回给客户端的响应（流式）


      cat 4_req_target.json | jq . | grep effort




```