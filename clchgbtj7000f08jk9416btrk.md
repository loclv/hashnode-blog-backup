# Cách tính connection pool size tham khảo từ Prisma ORM

Bàii viết tham khảo từ công thức:

* [https://www.prisma.io/docs/guides/performance-and-optimization/connection-management#recommended-connection-pool-size](https://www.prisma.io/docs/guides/performance-and-optimization/connection-management#recommended-connection-pool-size)
    
* [https://www.prisma.io/docs/concepts/components/prisma-client/working-with-prismaclient/connection-pool#connection-pool-size](https://www.prisma.io/docs/concepts/components/prisma-client/working-with-prismaclient/connection-pool#connection-pool-size)
    

## Ý nghĩa của Connection pool size

Connection pool size là con số để giới hạn lượng kết nối tới DB.

Càng lớn thì khi số lượng request lớn vẫn đảm bảo tốc độ trả về, nhưng lớn quá sẽ làm hạn chế performance, có nguy cơ quá số lượng cho phép.

Ngược lại, càng nhỏ thì số lượng request phải xếp hàng lại lớn nếu số lượng request lớn.

Cảnh xếp hàng, mỗi hàng như 1 Connection pool:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672823564982/736907ea-7bde-448d-af51-3a59023f2968.jpeg align="center")

\[image source\]([https://www.pexels.com/photo/teacher-in-yellow-cardigan-measuring-temperature-of-a-boy-in-face-mask-in-the-classroom-8363115/](https://www.pexels.com/photo/teacher-in-yellow-cardigan-measuring-temperature-of-a-boy-in-face-mask-in-the-classroom-8363115/))

## Cách tính

Đây là giới hạn từ ORM hay app instance (thực thể).

Cách tính như sau:

```plaintext
(num_physical_cpus * 2 + 1) ÷ number of application instances
```

Nếu số lượng ORM instance or App instance là 1 thì công thức sẽ trở thành:

```plaintext
num_physical_cpus * 2 + 1
```

Ví dụ, nếu DB server có 4 CPUs:

```plaintext
4 * 2 + 1 = 9
```

Kết quả là 9 connection pool.

Tại sao lại nhân số lượng nhân vật lý với 2? Có lẽ bởi vì \[two threads per core by default\]([https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-optimize-cpu.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-optimize-cpu.html)) - mặc định là mỗi 1 core sẽ có 2 threads chạy song song.

Để ý là \[mỗi vCPU của AWS sẽ tương đương với 1 thread, vậy 2 vCPUs mới là 1 physical CPU\]([https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-optimize-cpu.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-optimize-cpu.html)).

Ví dụ nếu ORM instance là 2 thì:

```plaintext
(4 * 2 + 1) / 2 = 9 / 2 = 4.5
```

Như vậy con số connection pool hợp lý ở đây là 4. Vì mỗi instance sẽ bị giới hạn là 4, tổng của cả 2 là `4 * 2 = 8`, con số này không vượt quá 9 như đã tính toán với 1 instance.

Tuy nhiên sẽ vẫn có nhiều biến số tùy vào bài toán thực tế, nên tốt nhất là ta phải thực hiện stress-test kết hợp monitoring DB, để xem mức chịu tải ra sao!