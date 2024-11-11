using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MovedPlayer : MonoBehaviour
{
    private Rigidbody2D _componentRigdbody2D;

    private float horizontal;
    private float vertical;
    public float speedx = 5f;
    public float speedy = 5f;

    private float screenWidth;
    private float screenHeight;

    private void Awake()
    {
        _componentRigdbody2D = GetComponent<Rigidbody2D>();
    }

    void Start()
    {
        screenWidth = Camera.main.aspect * Camera.main.orthographicSize;
        screenHeight = Camera.main.orthographicSize;
    }

    void Update()
    {
        horizontal = Input.GetAxis("Horizontal");
        vertical = Input.GetAxis("Vertical");
    }

    private void FixedUpdate()
    {
        Vector2 movement = new Vector2(horizontal * speedx, vertical * speedy);
        _componentRigdbody2D.velocity = movement;

        Vector3 pos = transform.position;
        pos.x = Mathf.Clamp(pos.x, -screenWidth, screenWidth);
        pos.y = Mathf.Clamp(pos.y, -screenHeight, screenHeight);
        transform.position = pos;
    }
}
