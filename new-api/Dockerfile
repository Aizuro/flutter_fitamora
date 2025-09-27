FROM python:3.9-bullseye  # ✅ Gunakan bullseye (Debian 11) yang stabil

# Install system dependencies for OpenCV
RUN apt-get update && apt-get install -y \
    libgl1 \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender1 \
    libx11-6 \
    libgomp1 \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy requirements first
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Verify installations
RUN python -c "import cv2; print('✅ OpenCV version:', cv2.__version__)"
RUN python -c "import mediapipe; print('✅ MediaPipe version:', mediapipe.__version__)"

# Expose port
EXPOSE 8080

# Start command
CMD ["gunicorn", "app:app", "--bind", "0.0.0.0:8080", "--workers", "2"]
