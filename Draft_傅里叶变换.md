## 1.问题引入：描述一条带有噪声的轨迹

我们任意给定一条关于时间$t$正弦轨迹$x_0(t)$：
$$
x_0(t)=\sin(4\pi t)
$$
对于$t\in[0, 1]$，按照每步$\delta t = 10^{-3}$为间隔取点，可以得到如下轨迹：

![controlTheory_sin0_traj](pics/controlTheory_sin0_traj.png)

但因为各种现实的因素，我们在真实环境中采集到的数据不可避免地存在噪声，假设我们用了两类传感器，分别采集到的信号如下：

![controlTheory_sin1_traj](pics/controlTheory_sin1_traj.png)

![controlTheory_sin2_traj](pics/controlTheory_sin2_traj.png)

可以看出，上面的两组带噪声轨迹，噪声的幅值和频率似乎都不相同，到底哪一组轨迹“好”，哪一组轨迹“坏”，似乎很难直接从图上看到。最简单的，我们可以把三组轨迹放在一起对比看一看：

![controlTheory_sin_traj_comp](pics/controlTheory_sin_traj_comp.png)

这样似乎显得更加迷惑了：直观上来说，$x_1$的噪声幅值似乎更大，$x_2$的噪声频率似乎更低（看起来噪声变化的比较慢），但如何准确的描述他们呢？

百年前的学者们研究出了在频域下描述轨迹的方法，发展到今天也就是常说的**傅里叶变换**，MATLAB官方提供了快速傅里叶变换的[接口](https://ww2.mathworks.cn/help/matlab/ref/fft.html?s_tid=doc_ta)`fft()`，我们将上述轨迹分别做傅里叶变换，结果如下：

![controlTheory_fft_comp](pics/controlTheory_fft_comp.png)

上图中横坐标为频率/Hz，纵坐标为幅值。不难看出，三组信号在时域上都是由频率为2Hz，幅值为1的正弦信号构成的，带有噪声的信号在频域图上也可以清晰的看出：$x_1$除了主信号外，还伴随着频率为50Hz，幅值为0.2的正弦信号；$x_2$除了主信号外，还伴随着频率为20Hz，赋值为0.1的正弦信号。

上面的结论量化评价了信号噪声的问题。可以看出，噪声在频域上的两个主要指标是频率和幅值，可以用傅里叶变换得到。