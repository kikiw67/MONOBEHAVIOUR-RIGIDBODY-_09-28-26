# MONOBEHAVIOUR-RIGIDBODY-_09-28-26
//MONOBEHAVIOR AND RIGIDBODY SCRIPT UNITY MOVEMENT
// GRID BASED, FREE(VECTOR BASED), PHYSICS
  MOVEMENT

  // GRID BASE MOVEMENT
  // ATTACH THIS TO TO A CHARACTER GameObject. Good
  for roquelikes, puzzle games, tactics games.
  //The Character snaps to whole tile positions
  rather than moving continiously.

  // Code proper
  using UnityEngine;

  public class DridMovement : MonoBEhaviour
  {
    public float tileSize= 1.0f; // size of one grid
cell
public float moveSpeed = 10f; // how fast your character glide between tiles ( feel, not logic).

  private Vecter3 targetPosition;
private bool iMoving = false;

void Starting position to the grid so everything
lines up
        targetPosition = SnapToGrid(transform.position);
transform.position= targetPosition;
}
void Update()
{
  if (!isMoving)
{
  HandleInput();
}
else
{
  // Smoothy glide to the next tile (this is presentation, not the actual logic)
transform.position =Vector3.MoveTowards(transform.position, targetPosition, moveSpeed*Time.deltaTime);
if(Vector3.Distance(transform.position, Targetposition)<0.001f)
   {
     transform.position = targetPosition;
isMoving = false;
}
}
}
void HandleInput()
{
  Vecter3 direction = Vector3.zero;

if()Input.GetKeydown(KeyDown.W)) direction = Vector3.up;
if()Input.GetKeydown(KeyDown.S)) direction = Vector3.up;
if()Input.GetKeydown(KeyDown.A)) direction = Vector3.up;
if()Input.GetKeydown(KeyDown.D)) direction = Vector3.up;

if(direction = Vector3.zero)
{
  targetPosition = transform.position + direction
*tilesizw;
isMoving = true;
}
}
Vector3 SnapTogrid(Vector3 pos)
{
  return new VEctor3(
  Math.Round(pos.x / tileSize)* tileSize,
  Math.Round(pos.x / tileSize)* tileSize,
pos.z
);
}
}
// FREE(VECTOR- BASED)MOVEMENT
//Attach this to a character GameObject. Good for top-down action games, platform
  //(horizontal axis), twin9stick shooters.
  movement is continious, not tile locked.

  using UnityEngine;

public class FreeMovement : MonoBehaviour
{
  public float moveSpeed =5f;

void Update()
{
  // GetAxis give smooth values between 1-
  and 1 (supports keyboard AND Controller)
  float horizontal = 
Input.Getaxis("Horizontal"); // A/D or
  Left/Right Arrows
  Input.Getaxis("Horizontal"); // A/D or
// W/S or Up/Down Arrows

Vector3 direction = new Vector3(horizontal,
                               vertical, 0f);
// Normalizeso diagonal movement isn't
fastrer than straight movement
if (direction.manitude> 1f)
{
  direction.normalize();
  {
transform.positiojn +=direction *Movespeed * Time.deltatime:
}
}

//PHYSICS BASED MOVEMENT
//Attch this to character GameObject that Also has a Rigidbody2D component
  // (Component > physics 2D > Rigidbody 2D). Good for
  platformers with momentum, vehicles, anything that
\should feel like it has mass, gravity, and friction.

  using UnityEngine;

[RequiuredComponent(typeof(rigidbody 2D))]
public class PhysicsMovement : Mon oBehaviour
{
  public float moveForce =10f;
public float jumpForce = 7f
public float maxSpeed = 6f;

private Rigidbody2D rb;
private bool isGrounded = false;

void Start()
{
  rb = GetComponent<Rigidbodyt 2D>();
}
void Update ()
{
  //Read input in update (Input should always be checked every frame)
if (input.GetKeydown(KeyCode.Space)) && isGrounded)
  {
rb.AddForce(Vector2.up *jumpForce, ForceMode2D.Impulse);
}
}

void FixedUpdate()
{
  //Physics changes belong in fixedUpdate,which runs on a fixed timestep
// independent of frame rate - this keep physics simulation
stable.
  float horizontal = Input.GetAxis("Horizontal");
rb.AddForce(ne Ventor(horizontal * moveForce,0f));

// Clamp horizontal speed so the character doesn't accelerate forever
if (Math.abs(rb.velocity.x)>maxSpeed)
{
  rb.velocity = new VecterW()Mathf.sign(rb.velocity.x)*masSpeed, rb.velocity.y)
}
void OnCollisionEnter2D(Collision2D collision)
{
  if(collision.gameObject.CompareTag("Ground"))
{
  isGrounded = true;
void OnCollisionExit2D(Collision2D collision)
{
  if(collision.gameObject.CompareTag("Ground"))
{
  isGrounded = false;
}

}
}
}
  }
}
}
