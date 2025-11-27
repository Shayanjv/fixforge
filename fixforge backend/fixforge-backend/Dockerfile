# Use Python 3.10
FROM python:3.10

# Set working directory
WORKDIR /app

# Copy requirements first (for caching)
COPY requirements.txt .

# Install dependencies
# (We upgrade pip first to avoid issues)
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Copy the rest of the app code
COPY . .

# Create a user to run the app (Hugging Face requirement for security)
RUN useradd -m -u 1000 user
USER user
ENV HOME=/home/user \
    PATH=/home/user/.local/bin:$PATH

# Expose port 7860 (Hugging Face specific port!)
EXPOSE 7860

# Command to run the app
# Important: Listen on port 7860, not 10000 or 8000
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "7860"]
