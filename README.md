{/* Background Music */}
    <audio autoPlay loop controls className="mx-auto">
      <source src="/audio/wedding.mp3" type="audio/mpeg" />
    </audio>

    <Card className="shadow-2xl rounded-2xl backdrop-blur bg-white/80">
      <CardContent className="space-y-6 p-6">
        <h1 className="text-2xl font-bold text-center" style={{ fontFamily: 'Playfair Display, serif' }}>
          RSVP for the Wedding of
        </h1>
        <h2 className="text-xl text-center" style={{ fontFamily: 'Great Vibes, cursive' }}>
          Muhammad Mahathir & Fatin Ellyana
        </h2>
        <p className="text-center">Date: November 23, 2025</p>
        <p className="text-center">Venue: Masjid Sri Sendayan</p>
        <p className="text-center text-sm">RSVP by October 26, 2025</p>

        <div className="text-center">
          <Countdown date={new Date('2025-11-23T00:00:00')} />
        </div>

        {submitted ? (
          <div className="text-green-600 text-center font-semibold">
            Thank you for your response!
          </div>
        ) : (
          <form onSubmit={handleSubmit} className="space-y-4">
            <div>
              <Label htmlFor="name">Your Name</Label>
              <Input id="name" name="name" value={formData.name} onChange={handleChange} required />
            </div>
            <div>
              <Label htmlFor="guests">Number of Guests</Label>
              <Input id="guests" name="guests" type="number" value={formData.guests} onChange={handleChange} required />
            </div>
            <div>
              <Label htmlFor="attending">Will you be attending?</Label>
              <select id="attending" name="attending" className="w-full p-2 rounded border" value={formData.attending} onChange={handleChange} required>
                <option value="">Select</option>
                <option value="yes">Yes</option>
                <option value="no">No</option>
              </select>
            </div>
            <Button type="submit" className="w-full">Submit RSVP</Button>
          </form>
        )}

        <p className="text-center text-sm text-gray-500">Contact: 010-3605824</p>

        {/* QR Code Placeholder */}
        <div className="text-center">
          <img src="/images/qr-code.png" alt="RSVP QR Code" className="w-24 mx-auto mt-4" />
          <p className="text-xs text-gray-400">Scan to RSVP</p>
        </div>
      </CardContent>
    </Card>
  </div>
</div>
