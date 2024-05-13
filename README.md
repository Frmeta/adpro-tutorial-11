## Refleksi Modul 11 Adpro


1. **Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?**

    Ya, terdapat perubahan yakni setelah meng-expose service, tiap request GET akan tercatat pada log. Setiap kali saya membuka aplikasi log tersebut akan bertambah. Berikut screenshoot perbedaan application logs sebelum dan setelah `kubectl service hello-node`:
    
    Before:
    ![alt text](image.png)

    After:
    ![alt text](image-1.png)


2. **Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?**

    Namespace dalam kubernetes adalah mekanisme untuk mengisolasi grup resource tertentu dalam satu cluster. Namespace dibuat ketika user-nya terpisah dari beberapa tim/projek.

    Ada dua versi `kubectl get`:
    - Tidak ada `-n`: artinya mengambil informasi secara default, yakni dari namespace tempat saya bekerja dalam cluster Kubernetes
    - Ada `-n`: n yang merupakan singkatan dari namespace ini mampu mengambil informasi berdasarkan namespace tertentu saja, pada tutorial ini informasi tersebut diambil hanya yang memiliki namespace `kube-system`.

    Output tidak menyebutkan pods/service yang telah saya buat karena berada dalam namespace `default`, bukan `kube-system`


## Reflection on Rolling Update & Kubernetes Manifest File

1. **What is the difference between Rolling Update and Recreate deployment strategy?**
    - Rolling Update: strategi deployment default yang digunakan Kubernetes dimana ketika kita mengupdate deployment, pods akan diupdate dengan cara perlahan-lahan menggantikan versi lama dari pod dengan bersi yang lebih baru. Dengan begitu, dapat dipastikan tidak ada waktu downtime. Selain itu apabila ada masalah dalam proses update, Kubernetes akan kembali rollback ke versi lama yang lebih stabil.
    - Recreate: strategi dimana semua pods yang ada harus diterminate terlbeih dahulu sebelum versi lebih baru dibuat. Akibatnya akan ada waktu downtime ketika proses update. Biasanya strategi ini dipakai ketika aplikasi kita tidak dapat menjalankan pod dengan versi lama dan baru dalam waktu yang sama.

2. **Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.**
Ya, saya berhasil menggunakan menerapkan Recreate deployment strategy dengan mengikuti tutorial https://dev.to/cloudskills/kubernetes-deployment-strategy-recreate-3kgn bagian manual recreate deployment.

3. **Prepare different manifest files for executing Recreate deployment strategy.**


4. **What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking `kubectl apply -f` command) to the cluster.**
5. **(Optional) Do the same tutorial steps, but on a managed Kubernetes cluster (e.g., GCP). You need to provision a Kubernetes cluster on Google Cloud Platform. Then, re-run the tutorial steps (Hello Minikube and Rolling Update) on the remote cluster. Document your attempt and highlight the differences and any issues you encountered.**