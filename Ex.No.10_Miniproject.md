# Ex.No: 10  Implementation of 2D/3D game in Unity
### DATE: 15.11.2025                                                                            
### REGISTER NUMBER : 212223240119
### AIM: 
To develop a 2D side-scrolling “Rock Blaster” game in Unity where the player controls a spaceship that shoots lasers to destroy incoming rocks using C# scripting and basic AI logic for object movement.
### Algorithm:
```
1. Initialize game window.
2. Load sprites and sounds.
3. Read user input.
4. Update player and enemy positions.
5. Detect collisions.
6. Draw all objects on screen.
7. Repeat until game ends.

```  
### Program:
```
PlayerShooting.cs
using UnityEngine;

public class PlayerShooting : MonoBehaviour
{
    public GameObject laserPrefab;
    public float shootCooldown = 0.25f;
    public float forwardOffset = 1.0f;
    public float downwardOffset = -0.25f;
    private float lastShotTime;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && Time.time > lastShotTime + shootCooldown)
        {
            Shoot();
            lastShotTime = Time.time;
        }
    }

    void Shoot()
    {
        Vector3 spawnPos = transform.position + new Vector3(forwardOffset, downwardOffset, 0f);
        Instantiate(laserPrefab, spawnPos, Quaternion.identity);
    }
}


```

```
Laser.cs
using UnityEngine;

public class Laser : MonoBehaviour
{
    public float speed = 10f;

    void Update()
    {
        transform.Translate(Vector2.right * speed * Time.deltaTime);
    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Rock"))
        {
            Destroy(other.gameObject);
            Destroy(gameObject);
        }
    }
}

```

```
spawnManager.cs
using UnityEngine;
using System.Collections;

public class spawnManager : MonoBehaviour
{
    public GameObject rock;

    void Start()
    {
        StartCoroutine(SpawnRocks());
    }

    IEnumerator SpawnRocks()
    {
        while (true)
        {
            yield return new WaitForSeconds(Random.Range(3f, 6f));
            Vector3 pos = new Vector3(Random.Range(12f, 15f), -3.4f, 0f);
            Instantiate(rock, pos, Quaternion.identity);
        }
    }
}


```

```
Rock.cs
using UnityEngine;

public class Rock : MonoBehaviour
{
    public float speed = 3f;

    void Update()
    {
        transform.Translate(Vector2.left * speed * Time.deltaTime);
    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player") || other.CompareTag("Laser"))
        {
            Destroy(gameObject);
        }
    }
}
```
### Output:
<img width="1481" height="933" alt="512589588-2226f375-4622-4b76-b1ac-9e9a373bb160" src="https://github.com/user-attachments/assets/9b848d66-e016-404a-ba34-31de4f544c96" />



### Result:
Thus, the 2D “Rock Blaster” game was successfully developed using Unity and implemented with AI-based random spawning and collision detection logic for dynamic gameplay.
