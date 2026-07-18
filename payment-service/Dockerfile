FROM python:3.14-slim 
WORKDIR /app
COPY requirements.txt .

#sensible python settings
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

#Install the dependencies specified in requirements.txt
RUN pip install -r requirements.txt

#Copy the rest of the application code to the working directory
COPY app ./app

#create and switch to a non-root user to run the application
RUN useradd --create-home --uid 10001 appuser
#RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

#Expose port 8000 to the outside world
EXPOSE 8000

#Run the uvicorn server to serve the FastAPI application
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]


