using UnityEngine;

public class BallController : MonoBehaviour
{
    public float speed = 10f;
    private Vector2 startTouchPosition, endTouchPosition;
    private Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        if (Input.touchCount > 0)
        {
            Touch touch = Input.GetTouch(0);

            if (touch.phase == TouchPhase.Began)
            {
                startTouchPosition = touch.position;
            }
            else if (touch.phase == TouchPhase.Ended)
            {
                endTouchPosition = touch.position;
                Vector2 swipeDelta = endTouchPosition - startTouchPosition;

                if (Mathf.Abs(swipeDelta.x) > Mathf.Abs(swipeDelta.y))
                {
                    if (swipeDelta.x > 0)
                        MoveRight();
                    else
                        MoveLeft();
                }
            }
        }
    }

    void MoveRight()
    {
        rb.velocity = new Vector3(speed, rb.velocity.y, rb.velocity.z);
    }

    void MoveLeft()
    {
        rb.velocity = new Vector3(-speed, rb.velocity.y, rb.velocity.z);
    }
}
