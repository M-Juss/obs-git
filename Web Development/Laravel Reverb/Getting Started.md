
### Laravel Reverb - is a web socket in Laravel environment that uses broadcast and  echo for reading and listening to Channels

###### How to use it in decoupled architecture (front-end and backend is seperated)?

### Backed Configuration
```php
laravel new backend 
// creates a fresh Laravel app
cd backend
//goes to directory
composer require laravel/reverb 
// Adds WebSocket (real-time) capability
php artisan reverb:install --no-interaction 
// Sets up broadcasting + Reverb config
php artisan queue:table
// Creates database tables for background jobs
php artisan migrate 
// apply changes
php artisan install:api
// create api.php fro decoupled archi

php artisan make:model Message -m
// creates model with migration

//in model
protected $fillable = ['message'];

//in migation file
public function up()
{
    Schema::create('messages', function (Blueprint $table) {
        $table->id();
        $table->text('message');
        $table->timestamps();
    });
}

php artisan migrate 
// to apply changes

php artisan make:event MessageSent
// Creates broadcast event

// in event

use Illuminate\Broadcasting\Channel;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;
use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Queue\SerializesModels;

class MessageSent implements ShouldBroadcast
{
    use Dispatchable, SerializesModels;

    public $message;

    public function __construct($message)
    {
        $this->message = $message;
    }

    public function broadcastOn()
    {
        return new Channel('chat'); // channel is like the room
    }
}

php artisan make:controller MessageController
// creates controller in which logic reside

// in models
use Illuminate\Http\Request;
use App\Models\Message;
use App\Events\MessageSent;

class MessageController extends Controller
{
    // GET messages (for page load)
    public function index()
    {
        return Message::latest()->get();
    }

    // POST message
    public function send(Request $request)
    {
        $request->validate([
            'message' => 'required|string'
        ]);

        // Save to DB
        $message = Message::create([
            'message' => $request->message
        ]);

        // Broadcast to others
        broadcast(new MessageSent($message))->toOthers();

        return response()->json($message);
    }
}


// in routes/api.php
use App\Http\Controllers\MessageController;

Route::get('/messages', [MessageController::class, 'index']);
Route::post('/messages', [MessageController::class, 'send']);


// REQUIRED TO RUN 
php artisan serve
// Runs Laravel API
php artisan queue:work
// Processes broadcast jobs
phop artisan reverb:start
// Runs WebSocket server
```

### Additional Infos

Channel - global / public room
PrivateChannel - room with auth
PresenceChannel - see # of user in the room

broadcast()->toOthers. - this ensures that your message does not duplicate or reflected to yours.

