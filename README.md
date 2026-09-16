# Wolfen Face API: Seamless Access Control
*Building AI course project*

## Summary
The Wolfen Face API is a seamless access control system that utilizes Computer Vision and Facial Recognition to authenticate users for private venues, studios, or exclusive clubs without the need for physical badges or QR codes.

## Background
Managing physical access to private spaces often relies on physical badges, tickets, or QR codes. These traditional methods are prone to being lost, forgotten, or fraudulently shared. This creates security vulnerabilities and slows down the entry process. This problem is extremely frequent in daily operations of gyms, clubs, and corporate offices. My motivation is to modernize this flow, creating a hands-free, secure, and futuristic experience.

## Data and AI techniques
This solution utilizes Computer Vision and Facial Recognition algorithms to authenticate users.
* The system maps facial landmarks from a live camera feed.
* It compares these live facial vectors against a pre-registered database of authorized members.
* The API calculates the similarity distance to verify identity in real-time.

## How is it used?
The user approaches an entrance equipped with a camera. The `wolfen-face-api` captures a frame, processes the facial data, and communicates with the backend management system. If the user is recognized, the system automatically triggers the gate or door to unlock, creating a completely frictionless check-in experience.

```python
import numpy as np
from scipy.spatial.distance import cosine

def authenticate_user(live_embedding, database_embeddings, threshold=0.4):
    """
    Calculates the cosine distance between the live camera face vector 
    and the stored authorized vectors.
    """
    for user_id, stored_embedding in database_embeddings.items():
        # Calculate cosine distance (lower is more similar)
        distance = cosine(live_embedding, stored_embedding)
        
        if distance < threshold:
            print(f"Access Granted: User {user_id}")
            return True, user_id
            
    print("Access Denied: Unrecognized face.")
    return False, None

## Challenges
* **Privacy and Compliance:** Handling biometric data requires strict adherence to privacy laws and secure database encryption.
* **Environmental Factors:** Poor lighting conditions or extreme camera angles can reduce recognition accuracy.
* **Spoofing:** A malicious actor might try to trick the camera using a high-resolution photo. This project currently does not fully solve the "photo spoofing" issue without depth sensors.

## What next?
The immediate next step is implementing "liveness detection" to ensure the camera is capturing a real 3D face, preventing spoofing. Ultimately, the goal is to package this API into a plug-and-play Docker container that can be easily integrated into any existing point-of-sale (POS) or attendance dashboard. I would need assistance with advanced anti-spoofing AI models to scale this securely.

## Acknowledgments
* Inspiration drawn from seamless access systems in modern tech hubs.
* Built utilizing standard Python data science and computer vision libraries.
