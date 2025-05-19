# Image-Reconstruction
Hybrid Model Deep Unrolled Network
Dataset The dataset consists of paired DICOM images: • Noisy CT scans (noisy_dir) • Clean CT scans (clean_dir) These are normalized  and optionally augmented using transformations like flips and rotations. Each sample is returned as a tuple of tensors with shape [1, H, W].

Residual U-Net Architecture • Encoder (Downsampling Path) Conv(1 → 32) + ReLU + ResidualBlock(32) MaxPool(2x2) Conv(32 → 64) + ReLU + ResidualBlock(64) MaxPool(2x2) • Bottleneck Conv(64 → 128) + ReLU + ResidualBlock(128) • Decoder (Upsampling Path) UpConv(128 → 64) + Concatenate with skip connection from encoder Conv(128 → 64) + ReLU + ResidualBlock(64) UpConv(64 → 32) + Concatenate with skip connection from encoder Conv(64 → 32) + ReLU + ResidualBlock(32) • Output Layer Final Conv(32 → 1) to predict the denoised image.

Training Configuration • Loss Function: Mixed Loss = 0.8MSE + 0.2(1 - SSIM) • Optimizer: AdamW • Scheduler: ReduceLROnPlateau

Evaluation Metrics • PSNR (Peak Signal-to-Noise Ratio) • SSIM (Structural Similarity Index) • MSE (Mean Squared Error)
