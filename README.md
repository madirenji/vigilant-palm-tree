# vigilant-palm-tree
Wedding RSVP Fatin &amp; Mahathir
from pathlib import Path
import zipfile

# Define export directory
export_dir = Path("/mnt/data/RSVP_Full_Website")
components_dir = export_dir / "app"
public_image_dir = export_dir / "public/images"
public_audio_dir = export_dir / "public/audio"

# Create directory structure
components_dir.mkdir(parents=True, exist_ok=True)
public_image_dir.mkdir(parents=True, exist_ok=True)
public_audio_dir.mkdir(parents=True, exist_ok=True)

# JavaScript code
jsx_code = """
import { useState } from 'react';
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";
import Countdown from 'react-countdown';

export default function RSVPWebsite() {
  const [formData, setFormData] = useState({ name: '', guests: '', attending: '' });
  const [submitted, setSubmitted] = useState(false);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    setSubmitted(true);
    console.log(formData);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 via-white to-blue-100 p-4">
      <div className="max-w-xl mx-auto space-y-6">
        {/* Photo Header */}
        <img src="/images/couple-photo.jpg" alt="Couple" className="rounded-xl shadow-lg w-full max-h-64 object-cover" />

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
  );
}
"""

# Write code to file
(components_dir / "page.jsx").write_text(jsx_code)

# Add placeholder image and audio
(public_image_dir / "couple-photo.jpg").write_text("COUPLE PHOTO PLACEHOLDER")
(public_image_dir / "qr-code.png").write_text("QR CODE PLACEHOLDER")
(public_audio_dir / "wedding.mp3").write_text("BACKGROUND MUSIC PLACEHOLDER")

# Zip the folder
zip_path = "/mnt/data/RSVP_Full_Website.zip"
with zipfile.ZipFile(zip_path, "w") as zipf:
    for path in export_dir.rglob("*"):
        zipf.write(path, path.relative_to(export_dir))

zip_path
